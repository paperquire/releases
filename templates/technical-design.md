# Overview

## Problem Statement

The current authentication system uses session-based cookies with a monolithic user store. As we migrate to a microservices architecture, each service needs to independently verify user identity without coupling to the auth database. This design document proposes migrating to JWT-based authentication with an OAuth 2.0 authorization server.

## Goals

- Decouple authentication from individual services
- Support single sign-on (SSO) across all platform services
- Enable fine-grained, scope-based authorization
- Maintain backward compatibility during the migration period

## Non-Goals

- Replacing the existing user registration flow (separate project)
- Adding social login providers (Phase 2)
- Multi-tenant isolation (out of scope)

# Architecture

## System Context

```
┌─────────────┐     ┌──────────────┐     ┌─────────────────┐
│   Browser    │────▶│  API Gateway  │────▶│  Auth Service   │
│   / Mobile   │     │  (Kong)       │     │  (OAuth 2.0)    │
└─────────────┘     └──────┬───────┘     └────────┬────────┘
                           │                       │
                    ┌──────▼───────┐        ┌──────▼────────┐
                    │  Service A   │        │  User Store   │
                    │  Service B   │        │  (PostgreSQL) │
                    │  Service C   │        └───────────────┘
                    └──────────────┘
```

## Token Architecture

### Access Token (JWT)

| Field | Type | Description |
|---|---|---|
| `sub` | string | User ID (UUID) |
| `iss` | string | Auth service URL |
| `aud` | string[] | Allowed service identifiers |
| `exp` | number | Expiration (15 minutes) |
| `scope` | string | Space-separated permission scopes |
| `roles` | string[] | User roles |

### Refresh Token

- Opaque token stored in HttpOnly cookie
- 30-day expiration with sliding window
- Rotation on each use (previous token invalidated)
- Stored hashed in PostgreSQL with device fingerprint

## API Design

### Token Endpoint

```
POST /oauth/token
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code
&code=AUTH_CODE
&redirect_uri=https://app.example.com/callback
&client_id=web-app
&code_verifier=PKCE_VERIFIER
```

### Token Introspection

```
POST /oauth/introspect
Authorization: Basic base64(client_id:client_secret)

token=ACCESS_TOKEN
```

# Data Model

## Schema Changes

| Table | Change | Migration |
|---|---|---|
| `users` | Add `mfa_enabled`, `mfa_secret` columns | Non-breaking, nullable |
| `oauth_clients` | New table | Create |
| `refresh_tokens` | New table | Create |
| `authorization_codes` | New table | Create |
| `sessions` (legacy) | Soft-deprecate | Add `migrated_at` column |

## Key Decisions

### Why JWT over opaque tokens?

JWTs allow services to verify tokens locally using the public key, eliminating a network round-trip to the auth service on every request. At our scale (2,000 req/s), this reduces p99 latency by approximately 12ms per request.

### Why PKCE?

All public clients (SPAs, mobile apps) must use PKCE to prevent authorization code interception attacks. This is recommended by OAuth 2.1 and required by our security team.

> [!warning]
> The implicit grant flow is deprecated and must not be used. All new integrations must use the authorization code flow with PKCE.

# Migration Plan

## Phase 1: Parallel Operation (Weeks 1–4)

- Deploy auth service alongside existing session system
- New API endpoints accept both session cookies and JWTs
- Internal services begin issuing JWTs for service-to-service calls

## Phase 2: Client Migration (Weeks 5–8)

- Web app migrates to OAuth 2.0 flow
- Mobile apps release update with JWT support
- Monitor dual-auth metrics; session usage should decline

## Phase 3: Cutover (Weeks 9–10)

- Disable session-based auth for API endpoints
- Maintain session support only for legacy admin tools
- Remove session middleware from all new services

# Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Token signing key compromise | Low | Critical | HSM-backed keys, automated rotation |
| Clock skew causes token rejection | Medium | Medium | 30-second grace period on expiration checks |
| Refresh token theft | Low | High | Token rotation, device binding, anomaly detection |
| Migration breaks existing clients | Medium | High | Feature flags, gradual rollout, instant rollback |
