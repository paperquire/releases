# PaperQuire Sample Templates

Ready-to-use Markdown samples for each built-in PaperQuire template. Download any file and render it with PaperQuire to see the template in action.

## Quick Start

### Desktop App
Open PaperQuire, paste the Markdown content, select the matching template from the sidebar, and click **Export PDF**.

### CLI
```bash
paperquire render technical-design.md --template technical-design --title "Auth Migration" --cover --toc
```

### MCP (AI Agents)
```json
{
  "tool": "render",
  "arguments": {
    "markdown": "...",
    "template": "tech-spec",
    "title": "My Document",
    "cover": true,
    "toc": true
  }
}
```

## Templates

### Enterprise & Technical

| File | Template ID | Best For |
|---|---|---|
| `tech-spec.md` | `tech-spec` | Technical specs, interface definitions, standards documents |
| `compliance-report.md` | `compliance-report` | SOC 2, ISO 27001, security assessments, regulatory filings |
| `technical-design.md` | `technical-design` | Technical design docs, RFCs, API specs |
| `architecture.md` | `architecture` | Architecture docs, system design, diagram-heavy specs |
| `functional-spec.md` | `functional-spec` | Integration specs, functional design docs, SOWs |
| `brd.md` | `brd` | Business requirements, scope documents |
| `executive-report.md` | `executive-report` | Board decks, executive summaries, quarterly reports |
| `project-plan.md` | `project-plan` | Project plans, roadmaps, status reports |
| `corporate-branded.md` | `corporate-branded` | Customer-facing deliverables, branded proposals |
| `minimal-clean.md` | `minimal-clean` | Memos, one-pagers, meeting notes |

### EU Regulatory & Compliance

| File | Regulation | Best For |
|---|---|---|
| `gdpr-dpia.md` | GDPR (Art. 35) | Data Protection Impact Assessments |
| `gdpr-ropa.md` | GDPR (Art. 30) | Records of Processing Activities |
| `eu-ai-act-conformity.md` | EU AI Act (2024/1689) | AI system conformity assessments |
| `dora-ict-risk.md` | DORA (2022/2554) | ICT risk management frameworks for financial entities |
| `nis2-cybersecurity.md` | NIS2 Directive (2022/2555) | Cybersecurity assessments for essential/important entities |
| `esg-sustainability.md` | CSRD / EU Taxonomy | ESG and sustainability disclosures |

## Learn More

- [Documentation](https://paperquire.com/docs/)
- [CLI Reference](https://paperquire.com/docs/cli.html)
- [MCP Integration](https://paperquire.com/docs/mcp.html)
