# Introduction

## Purpose

This Functional Specification Document (FSD) describes the detailed functional requirements for the Payment Gateway Integration between the Order Management System (OMS) and Stripe payment processing. It defines the behavior, interfaces, data flows, and error handling for all payment-related operations.

## Document Conventions

| Term | Definition |
|---|---|
| OMS | Order Management System (internal) |
| PGW | Payment Gateway (Stripe) |
| PSP | Payment Service Provider |
| PCI DSS | Payment Card Industry Data Security Standard |

# Functional Overview

## Process Flow

The payment lifecycle follows this sequence:

1. Customer selects items and proceeds to checkout
2. OMS creates a payment intent via PGW
3. Customer enters payment details in the hosted payment form
4. PGW processes the payment and returns authorization
5. OMS confirms the order and triggers fulfillment
6. Settlement occurs within 2 business days

## Use Cases

### UC-1: Process New Payment

**Actor**: Customer
**Precondition**: Cart contains at least one item; customer is authenticated
**Trigger**: Customer clicks "Pay Now"

| Step | Actor | System Response |
|---|---|---|
| 1 | Customer clicks Pay Now | OMS validates cart and calculates total |
| 2 | System | Creates Stripe PaymentIntent with amount, currency, metadata |
| 3 | System | Returns client secret to frontend |
| 4 | Customer enters card details | Stripe.js tokenizes card data (never touches OMS servers) |
| 5 | Customer confirms | Stripe processes payment, returns result |
| 6 | System | OMS receives webhook, updates order status |

**Postcondition**: Order status = "Paid", payment record created, confirmation email sent

### UC-2: Process Refund

**Actor**: Customer Support Agent
**Precondition**: Order is in "Paid" or "Fulfilled" status
**Trigger**: Agent initiates refund from admin panel

| Step | Actor | System Response |
|---|---|---|
| 1 | Agent selects order, clicks Refund | OMS displays refund form (full/partial) |
| 2 | Agent enters amount and reason | OMS validates amount ≤ original payment |
| 3 | System | Creates Stripe Refund object |
| 4 | System | Updates order status, notifies customer |

**Postcondition**: Refund processed, order status updated, audit log entry created

> [!important]
> Refunds exceeding $5,000 require manager approval. The system must enforce this threshold and route the request to the approval workflow.

# Interface Specifications

## API Endpoints

### Create Payment Intent

```
POST /api/v2/payments/intent
Authorization: Bearer <token>
Content-Type: application/json

{
  "orderId": "ORD-2026-001234",
  "amount": 14999,
  "currency": "usd",
  "customerId": "cus_ABC123",
  "metadata": {
    "orderSource": "web",
    "promoCode": "SUMMER20"
  }
}
```

**Response** (201 Created):

```json
{
  "paymentIntentId": "pi_XYZ789",
  "clientSecret": "pi_XYZ789_secret_ABC",
  "status": "requires_payment_method",
  "amount": 14999,
  "currency": "usd"
}
```

### Webhook Events

| Event | Description | Action |
|---|---|---|
| `payment_intent.succeeded` | Payment confirmed | Update order to "Paid", send confirmation |
| `payment_intent.payment_failed` | Payment declined | Update order to "Payment Failed", notify customer |
| `charge.refunded` | Refund processed | Update order, adjust inventory if applicable |
| `charge.dispute.created` | Chargeback filed | Flag order, notify finance team |

## Error Handling

| Error Code | HTTP Status | Description | Recovery |
|---|---|---|---|
| `card_declined` | 402 | Card was declined | Prompt customer to try another card |
| `expired_card` | 402 | Card has expired | Prompt customer to update card |
| `insufficient_funds` | 402 | Insufficient funds | Prompt customer to try another card |
| `processing_error` | 500 | Stripe processing error | Retry after 5 seconds, max 3 attempts |
| `rate_limit` | 429 | Too many requests | Exponential backoff |

# Data Requirements

## Payment Record Schema

| Field | Type | Required | Description |
|---|---|---|---|
| `id` | UUID | Yes | Internal payment record ID |
| `orderId` | string | Yes | Associated order |
| `stripePaymentIntentId` | string | Yes | Stripe reference |
| `amount` | integer | Yes | Amount in cents |
| `currency` | string(3) | Yes | ISO 4217 currency code |
| `status` | enum | Yes | pending, succeeded, failed, refunded |
| `customerId` | string | Yes | Internal customer ID |
| `createdAt` | timestamp | Yes | Record creation time |
| `updatedAt` | timestamp | Yes | Last status change |

## Compliance Requirements

- **PCI DSS Level 1**: Card data never touches OMS servers; all card handling via Stripe.js and Stripe Elements
- **Audit logging**: All payment operations logged with actor, timestamp, IP, and outcome
- **Data retention**: Payment records retained for 7 years per financial regulations
- **Encryption**: All API communication over TLS 1.3; sensitive fields encrypted at rest

# Testing Requirements

| Test Type | Scope | Environment |
|---|---|---|
| Unit tests | Payment service logic | CI pipeline |
| Integration tests | Stripe test mode API | Staging |
| End-to-end tests | Full checkout flow | Staging |
| Load tests | 500 concurrent payments | Performance env |
| PCI compliance scan | External vulnerability scan | Production |
