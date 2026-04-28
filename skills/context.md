<!-- Synced from: business-flows/ and concepts/ (2026-04-28) -->
<!-- Update this file when business rules or policies change -->

# Procurement Context — Business Knowledge for AI Skills

## 0. Company Profile

### Company Identity
- **Company Name:** ABC Co., Ltd.
- **Industry:** [to be filled — e.g., Manufacturing, Technology, Retail]
- **Company Size:** [to be filled — e.g., 500 employees, mid-size enterprise]
- **Headquarters:** 123 Sukhumvit Road, Khlong Toei, Bangkok 10110
- **Tax ID:** 0-1055-64001-23-4
- **Phone:** 02-xxx-xxxx
- **Email (General):** info@abc.co.th
- **Email (Procurement):** procurement@abc.co.th
- **Email (Purchase):** purchase@abc.co.th

### Procurement Scope
- **Categories Commonly Purchased:** IT Equipment, Office Equipment, Software, Professional Services
- **Procurement Type:** Primarily Indirect Procurement (operational expenses)
- **Currency:** THB (Thai Baht)
- **Preferred Vendor Regions:** Thailand (primary), Southeast Asia (secondary)
- **Business Language:** Thai (primary), English (secondary — for international vendors)

### Delivery Locations
| Location | Address | Use For |
|----------|---------|---------|
| Head Office | 123 Sukhumvit Road, Khlong Toei, Bangkok 10110 | IT Equipment, Office Supplies |
| Warehouse | Warehouse Floor 1, Zone B (Head Office building) | Bulk goods, inventory items |

### Budget & Approval Thresholds
| Amount (THB) | Approval Required |
|-------------|-------------------|
| Up to 100,000 | Procurement Manager |
| 100,001 – 500,000 | Procurement Manager + Department Manager |
| 500,001 – 1,000,000 | Procurement Manager + CFO |
| Over 1,000,000 | Procurement Manager + CFO + CEO |

### Procurement Principles
- Always seek competitive bids — minimum 3 vendors per sourcing round
- Prioritize total cost of ownership (TCO) over unit price alone
- Support vendor diversity — actively discover new vendors, do not over-rely on incumbents
- Maintain transparency and auditability in all procurement decisions
- Comply with all applicable Thai regulations and tax requirements

## 1. Personas

| Persona | Responsibilities | Involved In |
|---------|-----------------|-------------|
| Procurement Coordinator | Creates RFx, manages vendor communication, tracks sourcing | Step 2 (Sourcing) |
| Evaluation Committee | Scores vendor proposals, conducts due diligence | Step 3 (Vendor Selection) |
| Procurement Manager | Approves evaluations, ensures process compliance | Steps 2, 3, 8 |
| Warehouse Staff | Receives goods, inspects against PO, creates GRN | Step 6 (Delivery) |
| Finance / AP | Verifies invoices, 3-way match, processes payment | Step 7 (Invoice) |
| Procurement Analyst | Calculates vendor KPIs, monitors performance | Step 8 (Measurement), Dashboard |
| CFO | Final budget approval on evaluations and contracts | Steps 3, 4 |

## 2. P2P Cycle Summary

```
PR → RFI → RFQ/RFP → Scorecard → Contract → PO → GRN → Invoice → Vendor KPIs
         (Sourcing)   (Selection)                  (Delivery) (Payment) (Measurement)
              ↑                                                              |
              └──────────── Feedback Loop (performance → future sourcing) ───┘
```

Each step produces a document with a unique ID. Documents chain via foreign keys (e.g., GRN references a PO number).

## 3. RFx Decision Rules

| Condition | Use |
|-----------|-----|
| Don't know the market, need to explore | RFI (market survey, no pricing) |
| Specs are clear, need price comparison | RFQ (direct price request) |
| Complex solution, evaluate holistically | RFP (proposal with weighted scoring) |
| Known vendor pool, simple repeat purchase | Skip RFI, go direct to RFQ |

Typical flow for complex categories: Market Research → RFI → Shortlist (3-5 vendors) → RFQ or RFP → Evaluation → Award

### Alternative Sourcing (New Vendor Discovery)

In every sourcing round, the procurement agent must actively search for new vendors beyond the existing vendor master. This ensures competitive pricing and avoids over-reliance on incumbent suppliers.

**Process:**

```
PR Specs → Online Search → Collect Vendor Data → Identify Gaps → Plan Outreach Emails → Collect Responses → Merge with Existing Vendors → Selection
```

1. **Online Search** — search the web for suppliers matching the PR's product/material specifications. Look for manufacturers, distributors, and resellers.
2. **Data Collection** — for each discovered vendor, collect as much data as possible using the Vendor Master schema (Section 7). Fields to prioritize:
   - Company name and contact info (minimum required)
   - Product catalog / categories
   - Certifications
   - Approximate pricing (if publicly available)
   - Location and delivery capability
3. **Gap Identification** — identify which fields are missing per vendor. Missing data is acceptable — leave blank for follow-up via RFx.
4. **Email Planning** — for each new vendor with missing critical data, draft an outreach email. One vendor = one email. The email requests specific missing information:
   - Pricing and trade conditions (if not found online)
   - Certifications and compliance documents
   - Company background and references
   - Delivery lead times and terms
   - Any other data needed for the evaluation criteria in Section 4
5. **Merge** — combine discovered vendors with existing vendor master data into a unified candidate list for evaluation.

**Rules:**
- New vendors are tagged with `source: "discovered"` and `status: "pending"` (not yet in vendor master)
- Existing vendors are tagged with `source: "existing"` and carry their current status
- Missing data fields are explicitly marked as `null` with a `missingDataNote` explaining what is needed
- New vendors with incomplete data can still enter the selection process — they are scored on available data with gaps flagged
- The outreach email must be professional, specific to the vendor, and request only the data that is actually missing

### Email Follow-Up Loop (Vendor Outreach)

After the initial outreach email is sent, the procurement agent must process vendor replies and follow up until all required data is collected.

**Process:**

```
Receive Email → Read Content & Attachments → Extract Data → Update Vendor Profile → Check Completeness → [Complete?] → Yes: Ready for Selection / No: Reply Email → (loop)
```

1. **Read Vendor Reply** — read the email body and any attachments (PDF, Word, Excel, images). Extract all relevant data points.
2. **Update Vendor Profile** — fill in the previously missing fields with data extracted from the reply. Map data to the Discovered Vendor Schema and Vendor Master schema.
3. **Check Completeness** — compare the updated profile against the required fields for evaluation (Section 4 criteria). Determine what is still missing.
4. **If complete** — mark vendor as `dataComplete: true`. Vendor is ready for the selection process.
5. **If incomplete** — draft a follow-up reply email to the same vendor requesting only the remaining missing fields. Be specific about what is still needed. Reference what was already received to avoid re-requests.

**Rules:**
- Each follow-up email references the previous correspondence (keep thread context)
- Only request data that is actually still missing — never re-ask for data already received
- Be professional and concise — vendors should not feel interrogated
- Track the outreach round number (1st email, 2nd follow-up, 3rd follow-up, etc.)
- After 3 follow-up rounds with no response or incomplete data, mark vendor as `outreachStatus: "unresponsive"` and proceed to selection with available data
- Attachments may contain data in various formats — extract structured data from PDFs, images, spreadsheets

### Discovered Vendor Schema

```
vendorName, website, contactEmail, contactPhone,
source: "discovered",
status: "pending",
discoveredFrom: "URL or search description",
categories[], certifications[],
availableData: { pricing: true|false, certifications: true|false, companyProfile: true|false, deliveryTerms: true|false },
missingFields[]: "list of fields that need follow-up",
outreachEmailPlanned: true|false,
outreachStatus: "not_started|awaiting_reply|in_progress|complete|unresponsive",
outreachRound: 0,
dataComplete: true|false
```

## 4. Vendor Evaluation Rules

### Scoring Method
- Scale: 1.0 (poor) to 5.0 (excellent)
- Weighted total = sum of (score × weight / 100)
- Rank by weighted total — highest = rank 1
- Due diligence on top 2-3 vendors before final award

### Standard Evaluation Criteria

| Criteria | Typical Weight | How to Measure |
|----------|---------------|----------------|
| Price / TCO | 25% | Direct price comparison |
| Quality & Spec | 20% | Document/certification review |
| Delivery & Lead Time | 20% | Reference check, past GRN data |
| Financial Stability | 15% | Financial reports, years in business |
| After-Sales Service | 10% | Warranty, support terms in proposal |
| Compliance & Risk | 10% | ISO certs, audit results, risk score |

Weights are adjustable per category. **Must total 100%.**

### Score Definitions

| Score | Meaning |
|-------|---------|
| 5.0 | Excellent — exceeds requirements |
| 4.0 | Good — fully meets requirements |
| 3.0 | Acceptable — meets minimum |
| 2.0 | Below average — partially meets |
| 1.0 | Poor — does not meet |

### Two-Phase Evaluation (Existing vs New Vendors)

When the candidate list includes both existing vendors (with historical data) and discovered vendors (without), use a two-phase scoring method to ensure fair comparison.

**Phase 1 — Proposal-Based (80% of total weight)**

Scored equally for all vendors based on their proposal/quotation data:

| Criteria | Phase 1 Weight |
|----------|---------------|
| Price / TCO | 25% |
| Quality & Spec | 20% |
| Delivery & Lead Time (promised) | 15% |
| After-Sales Service | 10% |
| Compliance & Risk (certifications, audits) | 10% |

**Phase 2 — Track Record (20% of total weight)**

| Criteria | Phase 2 Weight | Existing Vendor | New Vendor |
|----------|---------------|-----------------|------------|
| Historical OTD & Fill Rate | 8% | Actual KPIs from GRN data | Reference check OR neutral 3.0 |
| Historical Quality (rejection rate) | 6% | Actual KPIs from GRN data | Reference check OR neutral 3.0 |
| Invoice Accuracy & Payment History | 6% | Actual KPIs from Invoice data | Reference check OR neutral 3.0 |

**Phase 2 scoring rules for new vendors:**
- If client references are provided → score based on reference quality (1.0–5.0)
- If certifications serve as proxy evidence (e.g., ISO 9001 for quality) → score up to 4.0
- If no references and no proxy evidence → assign neutral 3.0 ("meets minimum, unproven")
- Never assign below 3.0 for lack of data — that penalizes newness, not performance

**Final score calculation:**
```
Total = (Phase 1 weighted total × 0.80) + (Phase 2 weighted total × 0.20)
```

The 80/20 split is adjustable per policy. For categories where historical reliability is critical (e.g., production materials), Phase 2 weight may increase to 30-40%.

**This two-phase method may influence award alternatives:**
- If a new vendor wins Phase 1 but has neutral Phase 2 scores → recommend conditional award or pilot order
- If an existing vendor has strong Phase 2 but weaker Phase 1 → note the reliability advantage in the alternative's detailed reason
- The confidence score for new-vendor alternatives should reflect data completeness — lower confidence when based on partial data

### Decision Output Requirements

Every evaluation must produce:

1. **At least 3 alternative award options:**
   - (a) Single-vendor award to rank-1
   - (b) Single-vendor award to runner-up
   - (c) Line-by-line split award
   - Additional options when warranted (staggered delivery, pilot-then-scale, conditional award)

2. **For each alternative, document:**
   - Short reason (1-2 sentences)
   - Detailed reason (one paragraph: scoring, operational impact, risk, compliance, historical evidence)
   - Confidence (decimal 0.01–1.00, use the full range)

3. **Primary recommendation** — name which alternative, justify if not highest-confidence

4. **Full vendor profile** for recommended vendor(s): ID, legal name, address, tax ID, phone, email, bank account, categories, certifications, risk score, status

## 5. Vendor KPIs

### Delivery KPIs

| KPI | Formula | Target |
|-----|---------|--------|
| On-Time Delivery (OTD) | Orders delivered on time / Total orders × 100 | >= 95% |
| Lead Time Variance | Actual lead time − Promised lead time (avg) | < ±1 day |
| Fill Rate | Items delivered / Items ordered × 100 | >= 98% |

### Quality KPIs

| KPI | Formula | Target |
|-----|---------|--------|
| Rejection Rate | Items rejected / Total received × 100 | < 1% |
| Return Rate | Orders returned / Total orders × 100 | < 2% |
| Warranty Claim Rate | Claims / Total items × 100 | < 0.5% |

### Cost KPIs

| KPI | Formula | Target |
|-----|---------|--------|
| Price Variance | (Actual − Contract price) / Contract × 100 | < 3% |
| Invoice Accuracy | Correct invoices / Total invoices × 100 | >= 98% |
| Cost Savings vs Budget | (Budget − Actual) / Budget × 100 | > 0% |

### Compliance & Risk KPIs

| KPI | Formula | Target |
|-----|---------|--------|
| Compliance Score | Checklist: certs, audit, SLA adherence | >= 90% |
| Supplier Response Time | Avg response to RFx or issues | < 48 hours |
| Supplier Risk Score | Combined financial + operational + compliance | < threshold |

### Performance Feedback Loop

- High OTD + Low Defects → higher scores in future evaluations
- Consistent Price Variance → flag for contract renegotiation
- Low Compliance Score → may trigger removal from approved vendor list
- Repeated Warranty Claims → reduce quality score in next selection round

## 6. Policies & Configurable Settings

> Settings marked with `[CONFIG]` are adjustable per project, category, or policy update.
> Update these values when company policy changes. All skills read from this section.

### Financial
- `[CONFIG]` VAT rate: **7%**
- `[CONFIG]` Standard payment terms: **Net 30 days** after receiving goods and GRN
- `[CONFIG]` Late delivery penalty: **0.1% per day** (configurable per contract)
- Currency: THB (see Company Profile → Section 0)

### Evaluation Settings
- `[CONFIG]` Phase 1 (proposal-based) weight: **80%**
- `[CONFIG]` Phase 2 (track record) weight: **20%**
- `[CONFIG]` Scoring scale: **1.0–5.0**
- `[CONFIG]` Minimum vendors to shortlist: **3**
- `[CONFIG]` Target vendors to shortlist: **3–5**
- `[CONFIG]` Minimum alternative award options: **3**
- `[CONFIG]` Neutral score for new vendors (no data): **3.0**

### Vendor Management
- `[CONFIG]` High-risk threshold (riskScore): **>= 2.5**
- Blacklisted vendors: never include in RFx, never recommend for award
- Only vendors with status "active" may receive RFx or be awarded
- Every sourcing round must include a search for new alternative vendors — do not rely solely on existing vendor master
- New vendors with status "pending" may participate in evaluation but cannot be awarded until onboarded to "active"
- When comparing existing vs new vendors, clearly label the source and data completeness

### Outreach Settings
- `[CONFIG]` Max follow-up email rounds: **3**
- `[CONFIG]` Default response deadline: **14 calendar days**
- `[CONFIG]` Email language (Thai vendors): **Thai**
- `[CONFIG]` Email language (international vendors): **English**
- One email per vendor per round — never batch multiple vendors

### Approval Chains

**Vendor Selection:**
1. Evaluation Committee Chairman — validates scoring
2. Procurement Manager — confirms process compliance
3. CFO — final budget approval

**RFP:**
1. Procurement Manager
2. CTO / Project Owner
3. CFO

**Budget-based (see Company Profile → Section 0 for thresholds)**

### RFQ Quotation Conditions
- Prices must include VAT (7%) and be itemized per unit
- Warranty and on-site service terms must be specified
- Payment terms: Net 30 after GRN
- Delivery capability within specified timeframe
- Equivalent alternatives allowed with justification

## 7. Data Schemas

### Vendor Master
```
vendorId, vendorName, address, taxId, phone, email,
bankAccount: { bank, branch, accountNumber, accountName },
categories[], certifications[], status (active|blacklisted|pending),
riskScore, createdAt, updatedAt
```

### Purchase Requisition
```
prNumber, requestingDepartment, requesterId, requestDate, requiredDate,
procurementType (Direct|Indirect), category, budgetAllocation, budgetAmount, currency,
justification, lineItems[]: { itemNumber, itemName, specification, quantity, unit, estimatedUnitPrice },
estimatedTotal, approvalChain[]: { role, employeeId, status, date }, status
```

### RFI
```
rfiNumber, relatedPr, sentTo, issueDate, submissionDeadline,
coordinatorId, coordinatorEmail, category, objective,
informationRequested[], submissionFormat, submissionEmail, notes,
status, responsesReceived, shortlistedVendors[]
```

### RFQ
```
rfqNumber, relatedPr, relatedRfi, sentTo[], issueDate, submissionDeadline,
validityPeriod, category,
lineItems[]: { itemNumber, itemName, specification, quantity, unit },
quotationConditions[], status
```

### RFP
```
rfpNumber, projectName, budgetFrame: { amount, currency, includes },
submissionDeadline, resultAnnouncementDate, scopeOfWork[],
evaluationCriteria[]: { criteria, weight, scoringDetail },
requiredDocuments: { envelope1, envelope2, envelope3 },
approvalChain[], status
```

### Vendor Scorecard
```
scorecardId, relatedRfq, project, evaluationDate, committee[],
scoringScale: { min, max },
criteria[]: { name, weight },
vendorScores[]: { vendorId, vendorName, scores: {}, weightedTotal, rank, remarks },
decision: { awardedVendorId, awardedVendorName, nextStep },
approvalChain[]: { role, status }, status
```

### Purchase Order
```
poNumber, buyer: { companyName, address, taxId, phone, email },
vendorId, poDate, deliveryDeadline, deliveryDays, paymentTerms, deliveryLocation,
lineItems[]: { itemNumber, itemName, specification, quantity, unit, unitPrice, total },
subtotal, vatRate, vatAmount, grandTotal, currency, specialConditions[], status
```

### Goods Receipt Note
```
grnNumber, poReference, vendorId, receiptDate, receivedById, receiptLocation,
inspectionItems[]: { itemNumber, itemName, orderedQuantity, receivedQuantity,
  rejectedQuantity, condition (normal|partial|damaged), remarks },
threeWayMatchStatus: { po: {}, grn: {}, invoice: {} },
signatures[]: { role, employeeId }, status (received_full|received_partial|disputed)
```

### Tax Invoice
```
invoiceNumber, vendorId, issuedTo: { companyName, address, taxId },
invoiceDate, poReference, grnReference, paymentDueDate, paymentTerms,
lineItems[]: { itemNumber, itemName, quantity, unit, unitPrice, total },
notes, subtotal, vatRate, vatAmount, grandTotal, currency,
paymentInfo: { bank, branch, accountNumber, accountName, remittanceEmail },
threeWayMatchStatus: { po, grn, invoice, readyForPayment }, status
```

### Employee
```
employeeId, name, role, department, email, canApprove
```

## 8. ID Conventions

| Document | Pattern | Example |
|----------|---------|---------|
| PR | PR-YYYY-NNNN | PR-2024-0892 |
| RFI | RFI-YYYY-NNNN | RFI-2024-0031 |
| RFQ | RFQ-YYYY-NNNN | RFQ-2024-0078 |
| RFP | RFP-YYYY-NNNN | RFP-2024-0012 |
| Scorecard | SC-YYYY-NNNN | SC-2024-0078 |
| PO | PO-YYYY-NNNN | PO-2024-1102 |
| GRN | GRN-YYYY-NNNN | GRN-2024-0521 |
| Invoice | INV-[VENDOR]-YYYY-NNNN | INV-TP-2024-8821 |

Generate next sequential ID by reading existing records.
