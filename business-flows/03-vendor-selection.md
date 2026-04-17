# Step 3: Vendor Selection

## Overview

Vendor Selection is the process of evaluating and comparing proposals from multiple vendors to select the best fit. This step uses a **Vendor Scorecard / Evaluation Matrix** with weighted scoring to produce an objective, traceable, and defensible decision.

This is the most subjective step in the procurement process and is prone to bias. Structured scoring helps make the process transparent and auditable.

## Actors

- **Procurement Team** — facilitates the evaluation process
- **Evaluation Committee** — scores vendors (typically includes procurement + requesting department + finance)
- **Approvers** — committee chairman, procurement manager, CFO

## Process Steps

```
Collect Responses → Define Criteria & Weights → Score Each Vendor → Calculate Weighted Totals → Due Diligence → Award Decision
```

1. **Collect Responses** — gather all vendor responses from the RFQ/RFP
2. **Define Criteria & Weights** — set evaluation criteria and weights (total = 100%)
3. **Score Each Vendor** — rate each vendor per criteria on a defined scale (e.g., 1.0–5.0)
4. **Calculate Weighted Totals** — multiply scores by weights and sum
5. **Due Diligence** — verify top 2-3 vendors before final decision
6. **Award Decision** — select the winner and document justification

## Evaluation Criteria

Standard criteria used for vendor evaluation. Weights can be adjusted per category:

| Criteria | Description | Typical Weight | How to Measure |
|----------|-------------|---------------|----------------|
| Price / TCO | Unit price, shipping, setup, and Total Cost of Ownership | 25% | Direct comparison |
| Quality & Spec | Product/service meets defined spec, required certifications | 20% | Document review |
| Delivery & Lead Time | Ability to deliver on time, acceptable lead time | 20% | Reference check |
| Financial Stability | Credit score, revenue, years in business, going-concern risk | 15% | Financial report |
| After-Sales Service | Warranty, on-site support, response time | 10% | Proposal review |
| Compliance & Risk | Legal compliance, ISO standards, supply chain risk | 10% | Audit / checklist |

## Weighted Scoring Method

The most common and recommended approach:

1. Define criteria and weights (weights must total 100%)
2. Score each vendor on each criteria using a consistent scale (e.g., 1.0 to 5.0)
3. Calculate weighted score: `score x weight`
4. Sum all weighted scores for each vendor
5. Rank vendors by total weighted score — highest score is the preliminary winner
6. Conduct due diligence on top 2-3 vendors before final award

### Scoring Scale

| Score | Meaning |
|-------|---------|
| 5.0 | Excellent — exceeds requirements |
| 4.0 | Good — fully meets requirements |
| 3.0 | Acceptable — meets minimum requirements |
| 2.0 | Below average — partially meets requirements |
| 1.0 | Poor — does not meet requirements |

### Example Scorecard

Reference: Scorecard for RFQ-2024-0078 (IT Equipment — 4 items)

**Evaluation Committee:** Procurement + IT Manager + Finance

| Criteria | Weight | TechPlus | NextIT | ProGadget | iTrade |
|----------|--------|----------|--------|-----------|--------|
| Price / TCO | 25% | 4.8 | 4.2 | 4.5 | 3.9 |
| Quality & Spec | 20% | 4.5 | 4.8 | 4.0 | 4.2 |
| Delivery & Lead Time | 20% | 4.2 | 4.5 | 4.8 | 3.8 |
| Financial Stability | 15% | 4.5 | 4.0 | 3.8 | 4.2 |
| After-Sales Service | 10% | 4.8 | 4.5 | 4.2 | 4.0 |
| Compliance & Risk | 10% | 4.2 | 4.0 | 3.9 | 4.5 |
| **Weighted Total** | | **4.52** | **4.41** | **4.30** | **4.05** |

### Result Summary

- **TechPlus (4.52):** Best price, 3-year after-sales with on-site service — **Recommended for Award**
- **NextIT (4.41):** Highest quality, but price 8% higher and 28-day delivery
- **ProGadget (4.30):** Fastest delivery (14 days), but unclear after-sale service terms
- **iTrade (4.05):** Highest price overall — Not recommended

**Decision:** Award to TechPlus Co., Ltd. — proceed to PO issuance.

## Approval Chain

| Role | Responsibility |
|------|---------------|
| Evaluation Committee Chairman | Validates scoring and ranking |
| Procurement Manager | Confirms process compliance |
| CFO | Final budget approval |

## Related Documents

- Input: Vendor responses from [Step 2: Sourcing](02-sourcing.md)
- Output: Award decision feeds into [Step 4: Contract & Negotiation](04-contract-and-negotiation.md)

## Related Mock Data

- [vendor-scorecards.json](../mock-data/vendor-scorecards.json)
- [vendors.json](../mock-data/vendors.json)
