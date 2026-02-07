# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an **ArcKit architecture governance project** — not a software codebase. It generates architecture documents (markdown) for the **Tax Compliance AI & Revenue Intelligence Platform** at HM Revenue and Customs.

There is no build system, test suite, or application code. All work is done through ArcKit slash commands that generate governance artifacts.

## How to Work in This Repository

### ArcKit Slash Commands

All artifacts are produced via `/arckit.*` commands. The recommended execution order follows the 12-tier dependency hierarchy in `DEPENDENCY-MATRIX.md` (M=Mandatory, R=Recommended, O=Optional):

| Tier | Phase | Key Commands |
|------|-------|-------------|
| 0 | Foundation | `plan`, `principles` |
| 1 | Strategic Context | `stakeholders` |
| 1.5 | Risk Assessment | `risk` |
| 2 | Business Justification | `sobc` |
| 3 | Requirements | `requirements` |
| 3.5 | Strategic Planning | `platform-design`, `strategy` |
| 4 | Detailed Design | `data-model`, `dpia`, `research`, `wardley`, `roadmap`, `diagram`, `adr`, `datascout`, `data-mesh-contract` |
| 5 | Procurement | `sow`, `dos`, `gcloud-search`, `gcloud-clarify`, `evaluate` |
| 6 | Design Reviews | `hld-review`, `dld-review` |
| 7-8 | Implementation & Operations | `backlog`, `trello`, `servicenow`, `devops`, `mlops`, `finops`, `operationalize` |
| 9-10 | Quality & Compliance | `traceability`, `analyze`, `principles-compliance`, `service-assessment`, `tcop`, `ai-playbook`, `atrs`, `secure`, `mod-secure`, `jsp-936` |
| 11-12 | Reporting & Publishing | `story`, `pages` |

The most-consumed artifacts are `requirements` (37 commands), `principles` (21 commands), and `stakeholders` (22 commands).

### Key Conventions

- **Document IDs**: Format `ARC-{PROJECT_ID}-{TYPE}-v{VERSION}.md` (e.g., `ARC-001-REQ-v1.0.md`). Multi-instance types use `ARC-{PID}-{TYPE}-{NUM}-v{VERSION}.md`. Generate with `.arckit/scripts/bash/generate-document-id.sh`.
- **Type codes**: PRIN, STKE, REQ, RISK, SOBC, STRAT, PLAT, DATA, DPIA, RSCH, SOW, EVAL, TRAC, ANLZ, BKLG, SRVN, DVOP, MLOP, FNOP, OPER, RDMP, TCOP, AIPL, ATRS, SECD, MSBD, JSP9, SVCA, STRY. Multi-instance: ADR, DIAG, WARD, DMC.
- **Global artifacts** (principles) go in `projects/000-global/`
- **Project-specific artifacts** go in `projects/{PROJECT_ID}/` with subdirectories: `decisions/`, `diagrams/`, `wardley-maps/`, `data-contracts/`, `reviews/`, `external/`, `vendors/`, `final/`
- **Templates**: Default templates are provided by the ArcKit plugin. Custom overrides in `.arckit/templates/` or `.arckit/templates-custom/` take precedence. Always read the relevant template before generating a document.
- **Version** is in the `VERSION` file (currently 2.0.0) — include in generated document metadata
- **External documents**: Commands auto-discover user-provided files (vendor HLDs, policy docs, pen test reports) from `projects/{project}/external/`, `projects/{project}/vendors/{vendor}/`, and `projects/000-global/policies/`. These enhance output but are never required.

### Autonomous Agents

Research-heavy commands (`/arckit.research`, `/arckit.datascout`, `/arckit.aws-research`, `/arckit.azure-research`) delegate to autonomous agents that run in isolated context windows via the Task tool.

### MCP Integration

The ArcKit plugin bundles MCP servers for AWS Knowledge and Microsoft Learn for cloud research via `/arckit.aws-research` and `/arckit.azure-research`.

### Generated Artifacts (This Project)

No artifacts have been generated yet. Run `/arckit.principles` to begin, then follow the tier order in `DEPENDENCY-MATRIX.md`.

Expected artifacts for project 001 (Tax Compliance AI & Revenue Intelligence Platform):
- `ARC-000-PRIN-v1.0.md` — Global architecture principles
- `ARC-001-STKE-v1.0.md` — Stakeholder analysis
- `ARC-001-RISK-v1.0.md` — Risk register
- `ARC-001-SOBC-v1.0.md` — Strategic Outline Business Case
- `ARC-001-REQ-v1.0.md` — Requirements specification
- `ARC-001-DATA-v1.0.md` — Data model
- `ARC-001-DPIA-v1.0.md` — Data Protection Impact Assessment
- `ARC-001-TCOP-v1.0.md` — Technology Code of Practice Review
- `ARC-001-AIPL-v1.0.md` — AI Playbook Assessment
- `ARC-001-ATRS-v1.0.md` — ATRS Records
- `ARC-001-SECD-v1.0.md` — Secure by Design

## Project Context

HM Revenue and Customs (HMRC) collects over £800 billion in tax revenue annually and administers the UK's tax, payments, and customs systems. With over 45 million individual taxpayers and 6 million businesses, HMRC handles massive data volumes. AI can transform tax compliance, fraud detection, customer service, and the Making Tax Digital programme.

### Compliance Context

UK Government non-ministerial department. Applicable frameworks: GDS Service Standard, Technology Code of Practice (TCoP), NCSC Cyber Assessment Framework, ATRS for AI tools, UK GDPR (taxpayer data — highly sensitive), HM Treasury Green Book, AI Playbook, HMRC Charter, Finance Act provisions.

### Key Stakeholders

HMRC (service owner), taxpayers (individuals and businesses), tax agents and accountants, HMRC digital services, HM Treasury, Border Force (customs), Companies House, professional bodies (ICAEW, CIOT, ATT).
