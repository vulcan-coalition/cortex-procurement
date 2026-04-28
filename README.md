# Procurement Process Knowledge Base

This knowledge base documents the Procure-to-Pay (P2P) business domain for the development team. All content is derived from internal procurement training materials.

## Skills (AI Agent Prompts)

Prompt files for Claude Cowork. Each skill is a standalone instruction set that references `context.md` for business knowledge and connects to mock-data (or MCP) for data access.

**Usage in Cowork:** Load `context.md` as project context + one skill file per session.

### Flow

```
02-vendor-research → 02a-email-preparation → 02b-email-follow-up (loop) → 03-vendor-selection
                                                                                    ↓
                                                          08-vendor-measurement ← (after delivery & payment)
                                                                    ↓
                                                          09-status-dashboard
```

### Files

| File | Purpose |
|------|---------|
| [context.md](skills/context.md) | Shared context: company profile, personas, policies, business rules, data schemas |
| [02-vendor-research.skill.md](skills/02-vendor-research.skill.md) | Search existing + discover new vendors, gap analysis, RFx creation |
| [02a-email-preparation.skill.md](skills/02a-email-preparation.skill.md) | Draft outreach emails for vendors with missing data |
| [02b-email-follow-up.skill.md](skills/02b-email-follow-up.skill.md) | Process vendor email replies, extract data, follow up until complete |
| [03-vendor-selection.skill.md](skills/03-vendor-selection.skill.md) | Score vendors (two-phase: proposal + track record), produce ranked alternatives |
| [08-vendor-measurement.skill.md](skills/08-vendor-measurement.skill.md) | Calculate vendor KPIs from transaction data |
| [09-status-dashboard.skill.md](skills/09-status-dashboard.skill.md) | Vendor profile monitoring dashboard |

## Prompts (OpenAI Chat-Completion)

Standalone system prompts for single-call LLM engines (OpenAI, etc.). No file access, no tools — all data passed as JSON input, all results returned as JSON output.

| File | Purpose |
|------|---------|
| [02-vendor-research.prompt.md](prompts/02-vendor-research.prompt.md) | Research vendors, gap analysis, RFx creation |
| [02a-email-preparation.prompt.md](prompts/02a-email-preparation.prompt.md) | Draft outreach emails (email drafting only) |
| [02b-email-follow-up.prompt.md](prompts/02b-email-follow-up.prompt.md) | Process vendor replies, extract data, draft follow-ups |
| [03-vendor-selection.prompt.md](prompts/03-vendor-selection.prompt.md) | Two-phase vendor scoring with ranked alternatives |
| [08-vendor-measurement.prompt.md](prompts/08-vendor-measurement.prompt.md) | Calculate vendor KPIs from transaction data |
| [09-status-dashboard.prompt.md](prompts/09-status-dashboard.prompt.md) | Vendor profile monitoring dashboard |

### Skills vs Prompts

| | `skills/` | `prompts/` |
|---|---|---|
| Runtime | Claude Code / Cowork (multi-step, file access) | OpenAI chat-completion (single call, stateless) |
| Context | References `context.md` | Business rules embedded inline |
| Data | Reads mock-data files or MCP | All data in input JSON |
| Output | JSON + markdown summary | JSON only |

## Business Flows

The P2P cycle consists of 8 main processes:

| Step | Process | Document(s) | File |
|------|---------|-------------|------|
| 1 | Need Identification | PR (Purchase Requisition) | [01-need-identification.md](business-flows/01-need-identification.md) |
| 2 | Sourcing & RFx | RFI / RFQ / RFP | [02-sourcing.md](business-flows/02-sourcing.md) |
| 3 | Vendor Selection | Scorecard / Evaluation Matrix | [03-vendor-selection.md](business-flows/03-vendor-selection.md) |
| 4 | Contract & Negotiation | Contract / Framework Agreement | [04-contract-and-negotiation.md](business-flows/04-contract-and-negotiation.md) |
| 5 | Purchase Order | PO (Purchase Order) | [05-purchase-order.md](business-flows/05-purchase-order.md) |
| 6 | Delivery & Receipt | GRN (Goods Receipt Note) | [06-delivery-and-receipt.md](business-flows/06-delivery-and-receipt.md) |
| 7 | Invoice & Payment | Invoice / Payment Voucher | [07-invoice-and-payment.md](business-flows/07-invoice-and-payment.md) |
| 8 | Vendor Measurement | KPI Scorecard | [08-vendor-measurement.md](business-flows/08-vendor-measurement.md) |

Overview: [procurement-overview.md](business-flows/procurement-overview.md)

## Concepts

Foundational knowledge for understanding the procurement domain:

- [Supply Chain Overview](concepts/supply-chain-overview.md) — 3 flows (Material, Information, Money) and where procurement fits
- [Procurement vs Purchasing](concepts/procurement-vs-purchasing.md) — Strategic vs operational distinction
- [Direct vs Indirect Procurement](concepts/direct-vs-indirect-procurement.md) — Impact on process and data
- [Data Flow and Entities](concepts/data-flow-and-entities.md) — Systems, key data entities, and integration points

## Mock Data

Structured JSON files for use in application code. Each file corresponds to a document type in the P2P cycle:

| File | Document Type |
|------|--------------|
| [purchase-requisitions.json](mock-data/purchase-requisitions.json) | PR |
| [requests-for-information.json](mock-data/requests-for-information.json) | RFI |
| [requests-for-quotation.json](mock-data/requests-for-quotation.json) | RFQ |
| [requests-for-proposal.json](mock-data/requests-for-proposal.json) | RFP |
| [vendor-scorecards.json](mock-data/vendor-scorecards.json) | Scorecard |
| [purchase-orders.json](mock-data/purchase-orders.json) | PO |
| [goods-receipt-notes.json](mock-data/goods-receipt-notes.json) | GRN |
| [tax-invoices.json](mock-data/tax-invoices.json) | Invoice |
| [vendors.json](mock-data/vendors.json) | Vendor Master |
| [employees.json](mock-data/employees.json) | Employee / Approver |
