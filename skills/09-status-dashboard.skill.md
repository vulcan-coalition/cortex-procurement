# Vendor Status Dashboard — Procurement Skill

## Role

You are a Procurement Analyst. Refer to `context.md` → Section 1 (Personas) for your responsibilities.

## Context

Read `context.md` before executing. This is a read-only monitoring skill that aggregates vendor data into a profile dashboard. It supports decision-making across sourcing, vendor selection, and vendor measurement.

## Data Source

Read these mock-data files (will be replaced by MCP connection in future):

- `mock-data/vendors.json` — vendor profiles, categories, certifications, risk scores
- `mock-data/vendor-scorecards.json` — historical evaluation scores and rankings
- `mock-data/goods-receipt-notes.json` — delivery performance and inspection results
- `mock-data/tax-invoices.json` — invoice accuracy and payment status
- `mock-data/purchase-orders.json` — order history, pricing, delivery deadlines

Resolve `vendorId` across all files to aggregate per-vendor data. Use `poReference` in GRN to link to PO for delivery timeliness.

## Input

- **No input** → dashboard for all vendors
- **A vendor ID** (e.g., `VND-001`) → detailed profile for one vendor
- **A filter** (e.g., "high-risk vendors", "IT Equipment category") → filtered view

## Output Format

### All-Vendors Overview (default)

**Existing Vendors:**

| Rank | Vendor | Status | Risk | Categories | Certifications | Last Eval Score | OTD | Flags |
|------|--------|--------|------|------------|----------------|-----------------|-----|-------|

**Discovered Vendors (pending onboarding):**

If discovered vendor data exists from sourcing output, show:

| Vendor | Source | Categories | Data Completeness | Missing Fields | Outreach Status |
|--------|--------|------------|-------------------|----------------|-----------------|

### Single-Vendor Detail

**1. Profile Summary**

| Field | Value |
|-------|-------|
| Vendor ID | ... |
| Legal Name | ... |
| Status | active / blacklisted / pending |
| Categories | ... |
| Certifications | ... |
| Risk Score | X.X (Low < 1.5 / Medium < 2.5 / High >= 2.5) |
| Vendor Since | ... |

**2. Performance Snapshot**

Calculate KPIs using formulas from `context.md` → Section 5 (Vendor KPIs):

| KPI | Value | Target | Status |
|-----|-------|--------|--------|
| On-Time Delivery | X% | >= 95% | Pass/Fail |
| Fill Rate | X% | >= 98% | Pass/Fail |
| Rejection Rate | X% | < 1% | Pass/Fail |
| Invoice Accuracy | X% | >= 98% | Pass/Fail |
| Price Variance | X% | < 3% | Pass/Fail |

**3. Evaluation History**

| Scorecard | Project | Date | Score | Rank |
|-----------|---------|------|-------|------|

**4. Flags & Alerts**

List: high risk, partial deliveries, rejections, blacklisted, missing certifications, overdue payments.

## Chaining

Based on findings, suggest:
- Underperforming vendor → run `08-vendor-measurement.skill.md` for detailed KPI analysis
- New sourcing need → run `02-sourcing.skill.md`
- Vendor comparison → run `03-vendor-selection.skill.md`
