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

## Learn More

- [Documentation](https://paperquire.com/docs/)
- [CLI Reference](https://paperquire.com/docs/cli.html)
- [MCP Integration](https://paperquire.com/docs/mcp.html)
