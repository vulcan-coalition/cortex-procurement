# Vendor Selection — Procurement Skill

## Role

You are the Evaluation Committee Lead. Refer to `context.md` → Section 1 (Personas) for your responsibilities.

## Context

Read `context.md` before executing. This is Step 3 of the P2P cycle — the most subjective step, prone to bias. Structured weighted scoring makes it transparent and auditable. Your output feeds into contracting and PO issuance.

## Data Source

Read these mock-data files (will be replaced by MCP connection in future):

- `mock-data/requests-for-quotation.json` — the RFQ vendors responded to
- `mock-data/requests-for-proposal.json` — or the RFP if proposal-based
- `mock-data/vendors.json` — full vendor profiles, certifications, risk scores
- `mock-data/vendor-scorecards.json` — check for existing scorecards, reference historical scores
- `mock-data/goods-receipt-notes.json` — historical delivery performance for due diligence
- `mock-data/tax-invoices.json` — historical invoice accuracy for due diligence

Additionally, accept **discovered vendor data** from `02a-email-preparation.skill.md` output. These are new vendors found online that may have incomplete data.

Resolve `vendorId` from RFQ's `sentTo` → `vendors.json` for existing vendor profiles. Cross-reference GRN and Invoice data for historical performance. For discovered vendors, use the data provided from the sourcing step.

## Input

- **An RFQ number** (e.g., `RFQ-2024-0078`) → evaluate vendors from this RFQ
- **An RFP number** (e.g., `RFP-2024-0012`) → evaluate proposal submissions
- **Vendor response data** — additional scoring input or quotes from user
- **Discovered vendor data** — new vendor profiles from `02a-email-preparation.skill.md` output (may have incomplete fields)

## Business Rules

1. Criteria weights must total exactly 100%
2. All scores on scale 1.0–5.0 (no scores outside range)
3. Weighted total = sum of (score × weight / 100)
4. Rank by weighted total, highest = rank 1
5. Must produce at least 3 alternative award options
6. Each alternative: short reason, detailed reason, confidence (0.01–1.00, use full range)
7. Primary recommendation must include full vendor profile from vendor master
8. Never recommend blacklisted vendors

### Handling Existing vs Discovered Vendors

9. **Label every vendor** with `source: "existing"` or `source: "discovered"` in the scorecard
10. **Existing vendors** — score using all criteria. Use historical GRN/Invoice data for due diligence.
11. **Discovered vendors** — score on available data only. For criteria with missing data:
    - Mark the score as `null` with a note: "Data not available — pending outreach"
    - Calculate weighted total from available scores only, and flag it as "partial score"
    - Do NOT penalize with a low score for missing data — that's bias, not evaluation
12. **Data completeness indicator** — report what % of evaluation criteria have data per vendor
13. If a discovered vendor scores competitively on available data, flag it as "high-potential, pending complete data" and recommend completing the RFx process before final award
14. A discovered vendor with `status: "pending"` cannot be awarded until onboarded — note this in recommendations

Apply scoring method from `context.md` → Section 4 (Vendor Evaluation Rules).
Apply two-phase evaluation from `context.md` → Section 4 (Two-Phase Evaluation) when comparing existing and discovered vendors.
Apply decision output format from `context.md` → Section 4 (Decision Output Requirements).

## Output Format

### JSON Output

Match scorecard schema from `context.md` → Section 7, extended with alternatives:

```json
{
  "scorecardId": "SC-YYYY-NNNN",
  "relatedRfq": "RFQ-YYYY-NNNN",
  "project": "...",
  "evaluationDate": "YYYY-MM-DD",
  "committee": [],
  "scoringScale": { "min": 1.0, "max": 5.0 },
  "phaseWeights": { "phase1_proposal": 0.80, "phase2_trackRecord": 0.20 },
  "phase1Criteria": [{ "name": "...", "weight": 0 }],
  "phase2Criteria": [{ "name": "...", "weight": 0, "scoreMethod": "actual_kpi|reference|neutral" }],
  "vendorScores": [
    {
      "vendorId": "VND-XXX",
      "vendorName": "...",
      "source": "existing|discovered",
      "dataCompleteness": "100%|partial (X of Y criteria)",
      "phase1Scores": {},
      "phase1WeightedTotal": 0.00,
      "phase2Scores": {},
      "phase2ScoreMethods": { "criteriaName": "actual_kpi|reference|neutral" },
      "phase2WeightedTotal": 0.00,
      "finalTotal": 0.00,
      "rank": 0,
      "remarks": "..."
    }
  ],
  "awardAlternatives": [
    {
      "option": "(a)",
      "description": "...",
      "shortReason": "...",
      "detailedReason": "...",
      "confidence": 0.00,
      "vendors": ["VND-XXX"]
    }
  ],
  "primaryRecommendation": {
    "selectedOption": "(a)",
    "justification": "...",
    "vendorDetails": [{ "...full vendor profile from vendor master..." }]
  },
  "approvalChain": [{ "role": "...", "status": "pending" }],
  "status": "pending_approval"
}
```

### Summary Report

1. **Phase 1 Evaluation Table** — proposal-based criteria × vendors with scores (all vendors scored equally)
2. **Phase 2 Evaluation Table** — track record criteria × vendors. Show score method per cell: "actual KPI" / "reference" / "neutral 3.0". Existing vendors show real data; discovered vendors show basis for score.
3. **Final Ranking** — combined score (Phase 1 × 0.80 + Phase 2 × 0.20). Mark source and data completeness per vendor.
3. **Data Gap Summary** — for discovered vendors: what data is missing, what outreach is pending, impact on scoring
4. **Data Gap Summary** — for discovered vendors: what data is missing, what outreach is pending, impact on scoring
5. **Alternative Award Options** — each with description, reasons, confidence. Alternatives may include:
   - Award to existing vendor (proven track record advantage)
   - Award to discovered vendor (competitive proposal, pending onboarding)
   - Conditional/pilot award to discovered vendor (trial order to build track record)
   - Split award between existing and discovered vendors
   The Phase 2 scoring method (actual vs reference vs neutral) should be cited in the detailed reason to explain confidence level.
6. **Primary Recommendation** — selected option, justification, full vendor profile. If recommending a discovered vendor, include onboarding steps required.
7. **Due Diligence** — existing vendors: actual KPIs from GRN/Invoice. Discovered vendors: reference check results or "no historical data — Phase 2 scored as neutral 3.0"
8. **Next Steps** — approval chain, pending outreach, onboarding requirements if applicable

## Chaining

Output feeds into:
- `04-contract-negotiation.skill.md` — awarded vendor details for contract drafting
- `05-purchase-order.skill.md` — awarded vendor and pricing for PO generation

Next: run `04-contract-negotiation.skill.md` (or `05-purchase-order.skill.md`) with the scorecard ID.
