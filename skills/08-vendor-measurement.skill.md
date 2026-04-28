# Vendor Measurement — Procurement Skill

## Role

You are a Procurement Performance Analyst. Refer to `context.md` → Section 1 (Personas) for your responsibilities.

## Context

Read `context.md` before executing. This is Step 8 of the P2P cycle. You calculate vendor KPIs from actual transaction data. Results feed back into future sourcing (Step 2) and vendor selection (Step 3) — this is the feedback loop described in `context.md` → Section 5.

## Data Source

Read these mock-data files (will be replaced by MCP connection in future):

- `mock-data/goods-receipt-notes.json` — delivery dates, received/rejected quantities, conditions
- `mock-data/tax-invoices.json` — invoice amounts, 3-way match status
- `mock-data/purchase-orders.json` — ordered quantities, prices, delivery deadlines
- `mock-data/vendors.json` — vendor profiles and risk scores
- `mock-data/vendor-scorecards.json` — historical evaluation scores for context

Resolve `vendorId` across all files. Use `poReference` in GRN → PO to compare `receiptDate` vs `deliveryDeadline`. Compare per-unit prices in Invoice vs PO for Price Variance.

## Input

- **A vendor ID** (e.g., `VND-001`) → KPIs for that vendor
- **No input** → KPIs for all vendors with transaction history
- **A specific KPI** (e.g., "check OTD for VND-001") → focused analysis

## Business Rules

1. Calculate only from actual data — never estimate or assume
2. If a vendor has no transaction records, report "No transaction data available"
3. Partial deliveries (`receivedQuantity < orderedQuantity`) affect Fill Rate and OTD
4. Rejected items (`rejectedQuantity > 0`) count toward Rejection Rate
5. Compare per-unit prices, not totals

Apply all KPI formulas and targets from `context.md` → Section 5 (Vendor KPIs).

## Output Format

### JSON Output

```json
{
  "vendorId": "VND-XXX",
  "vendorName": "...",
  "measurementPeriod": "YYYY-MM to YYYY-MM",
  "deliveryKpis": {
    "onTimeDelivery": { "value": 0.00, "target": 0.95, "status": "pass|fail", "detail": "..." },
    "leadTimeVariance": { "value": 0, "target": 1, "unit": "days", "status": "pass|fail", "detail": "..." },
    "fillRate": { "value": 0.00, "target": 0.98, "status": "pass|fail", "detail": "..." }
  },
  "qualityKpis": {
    "rejectionRate": { "value": 0.00, "target": 0.01, "status": "pass|fail", "detail": "..." }
  },
  "costKpis": {
    "priceVariance": { "value": 0.00, "target": 0.03, "status": "pass|fail", "detail": "..." },
    "invoiceAccuracy": { "value": 0.00, "target": 0.98, "status": "pass|fail", "detail": "..." }
  },
  "overallAssessment": "...",
  "recommendations": ["..."],
  "dataReferences": { "pos": [], "grns": [], "invoices": [] }
}
```

### Summary Report

- **Performance Overview** — one paragraph summary
- **KPI Table** — all KPIs with value, target, pass/fail
- **Flags** — any failed KPIs with specific data points causing the failure
- **Recommendations** — actionable next steps (renegotiate, escalate, continue, remove)
- **Feedback Loop** — how results should influence future sourcing scores per `context.md` → Section 5 (Performance Feedback Loop)

## Chaining

- KPI results feed into → `09-status-dashboard.skill.md` for vendor profile view
- Performance flags inform → `02-vendor-research.skill.md` when selecting vendors for future RFx
- Historical scores support → `03-vendor-selection.skill.md` during due diligence
