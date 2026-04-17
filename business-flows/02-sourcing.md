# Step 2: Sourcing & RFx

## Overview

Sourcing is the process of finding and evaluating potential suppliers for goods or services. The procurement team analyzes the requirement from the approved PR and selects the appropriate sourcing method. This step produces RFx documents — RFI, RFQ, and/or RFP — depending on how well the organization understands the market and the complexity of the purchase.

## Actors

- **Procurement Team** — leads the sourcing process, creates and distributes RFx documents
- **Vendors / Suppliers** — receive RFx documents and submit responses
- **Requester** — provides specifications and clarification on requirements

## When to Use Which RFx

| Document | When to Use | What You Need | What You Get |
|----------|------------|---------------|-------------|
| RFI | Don't know the market, need to explore first | Vendor capabilities and experience | Supplier long list |
| RFQ | Specs are clear, just need prices | Prices and lead times for defined items | Price comparison table |
| RFP | Complex solution needed, evaluate holistically | Approach, technology, team, and pricing | Proposals scored on multiple criteria |

## Typical Sourcing Flow

For complex categories, sourcing typically follows this flow:

```
Market Research → RFI → Shortlist → RFQ or RFP → Evaluation → Award
```

1. **Market Research** — study the category to understand available suppliers and price ranges
2. **RFI Distribution** — send to multiple vendors to survey capabilities
3. **Shortlist** — narrow down to 3-5 most promising vendors from RFI responses
4. **RFQ or RFP** — send to shortlisted vendors only for detailed information
5. **Evaluation** — assess responses against predefined criteria
6. **Award** — notify the winner and proceed to contract

For simpler purchases with known specs and established vendor relationships, the flow may skip RFI and go directly to RFQ.

## RFI — Request for Information

### Purpose

Market survey. Not a price request — no legal obligation. The goal is to understand what vendors exist, what they can do, and to build a shortlist for the next step.

### Key Fields

| Field | Description |
|-------|------------|
| RFI Number | Unique identifier (e.g., RFI-2024-0031) |
| Sent To | Target audience (e.g., Open Market, specific vendors) |
| Issue Date | Date RFI is published |
| Submission Deadline | Last date to receive vendor information |
| Coordinator | Contact person in procurement |
| Objective | What the organization wants to learn |
| Information Requested | Specific questions for vendors |
| Submission Format | PDF, Word, etc. |

### Information Typically Requested

1. Experience in supplying the category for organizations (years in business, number of clients)
2. Brands and models available with specs
3. After-sales services: warranty period, on-site service, response time
4. Approximate pricing (non-binding)
5. Certifications: ISO, safety standards
6. Company information: registration, contacts, website

### Expected Outcome

Shortlist of 3-5 vendors to proceed with RFQ.

## RFQ — Request for Quotation

### Purpose

Price comparison. Specs are clear and defined — this is a straightforward "give us your best price" request. Sent only to shortlisted vendors.

### Key Fields

| Field | Description |
|-------|------------|
| RFQ Number | Unique identifier (e.g., RFQ-2024-0078) |
| Sent To | Shortlisted vendors from RFI or approved vendor list |
| Issue Date | Date RFQ is published |
| Submission Deadline | Last date/time for price submission |
| Validity Period | How long the quoted price must remain valid (e.g., 30 days) |
| Items | List of items with specifications, quantities, and units |

### Quotation Conditions

- Prices must include VAT (7%) and be itemized per unit
- Warranty and on-site service terms must be specified
- Payment terms: e.g., Net 30 days after receiving goods and GRN
- Delivery capability within specified timeframe
- If unable to match the exact spec, provide equivalent alternatives with justification

### Line Items Structure

Each item in an RFQ includes:

| Field | Description |
|-------|------------|
| Item Number | Sequential number |
| Item Name | Product/service name |
| Specification | Detailed technical spec defined by buyer |
| Quantity | Required quantity |
| Unit | Unit of measure |
| Unit Price | Vendor fills in |
| Total (incl. VAT) | Vendor fills in |

### Signature Requirements

- Quotation submitter / Supplier representative
- Authorized signatory
- Company stamp

## RFP — Request for Proposal

### Purpose

Holistic evaluation. Used when the purchase involves complex solutions (e.g., software systems, consulting services) where price alone is not sufficient for decision-making. Evaluates solution + price together.

### Key Fields

| Field | Description |
|-------|------------|
| RFP Number | Unique identifier (e.g., RFP-2024-0012) |
| Project Name | Name of the project being sourced |
| Budget Frame | Maximum budget including implementation and licensing |
| Submission Deadline | Last date/time for proposal submission |
| Result Announcement Date | When the decision will be communicated |

### Scope of Work

The RFP defines the full scope that vendors must address. Example for an e-Procurement system:

1. Vendor Management: onboarding, KYC, blacklist check, performance scoring
2. RFx Management: create RFI/RFQ/RFP, auto-send, receive responses, evaluate
3. Contract Management: templates, digital signature, renewal alerts
4. PO Management: create PO, approval workflow, GRN matching
5. Dashboard & Reporting: KPI vendor, spend analysis, savings report
6. Integration: SAP ERP, Active Directory (SSO), email gateway

### Evaluation Criteria

| Criteria | Weight | Scoring Detail |
|----------|--------|---------------|
| Price / TCO (3 years) | 25% | Lowest price = 25 points, others proportional |
| Functionality & Features | 25% | Scope coverage >= 90% = full marks, live demo |
| Implementation Plan | 20% | Timeline, methodology, resources, risk plan |
| Support & SLA | 15% | Response time, uptime SLA, training plan |
| Vendor Financial Stability | 10% | Revenue history (3 years), headcount, references |
| Security & Compliance | 5% | ISO 27001, PDPA compliance, penetration test |

### Required Submission Documents

Proposals are typically submitted in sealed envelopes:

1. **Envelope 1 (Qualifications):** company certificates, past project references (min. 3), team CVs
2. **Envelope 2 (Technical):** technical proposal, architecture diagram, demo environment URL
3. **Envelope 3 (Commercial):** commercial proposal broken down by license, implementation, support/year

### Approval Chain

- Procurement Manager
- CTO / Project Owner
- CFO

## Related Documents

- Input: Approved PR from [Step 1: Need Identification](01-need-identification.md)
- Output: Vendor responses feed into [Step 3: Vendor Selection](03-vendor-selection.md)

## Related Mock Data

- [requests-for-information.json](../mock-data/requests-for-information.json)
- [requests-for-quotation.json](../mock-data/requests-for-quotation.json)
- [requests-for-proposal.json](../mock-data/requests-for-proposal.json)
