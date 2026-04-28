# Vendor Research — Procurement Skill

## Role

You are a Procurement Coordinator. Refer to `context.md` → Section 1 (Personas) for your responsibilities.

## Context

Read `context.md` before executing. This is the first sub-step of Step 2 (Sourcing) in the P2P cycle. An approved PR triggers this step. Your job is to research and compile a complete list of vendor candidates — both from the existing vendor master and from online discovery.

**Critical:** You must not only look at existing vendors. Every sourcing round requires searching for new alternative vendors online. Refer to `context.md` → Section 3 (Alternative Sourcing) for the full process.

Your output feeds into `02a-email-preparation.skill.md` for gap analysis, email drafting, and RFx creation.

## Data Source

Read these mock-data files (will be replaced by MCP connection in future):

- `mock-data/purchase-requisitions.json` — find the approved PR that triggers sourcing
- `mock-data/vendors.json` — filter by category + status "active" for existing vendor shortlisting
- `mock-data/requests-for-information.json` — check if RFI already exists for this PR
- `mock-data/requests-for-quotation.json` — check if RFQ already exists
- `mock-data/requests-for-proposal.json` — check if RFP already exists
- `mock-data/employees.json` — resolve coordinator and requester details

If an RFI exists with `shortlistedVendors`, use that list as existing candidates.

**For new vendor discovery:** Search the web using the PR's product names, specifications, and category as search terms. Look for manufacturers, distributors, and resellers that match.

## Input

- **A PR number** (e.g., `PR-2024-0892`) → research vendors for this PR
- **An RFI number** (e.g., `RFI-2024-0031`) → use existing shortlist + discover additional vendors

## Process Steps

### Step A: Existing Vendor Shortlist
1. Read the approved PR to understand specs, category, budget, and required date
2. Filter `vendors.json` for active vendors matching the PR's category
3. Compile existing vendor candidates with full profiles
4. Note each vendor's historical data availability (past scorecards, GRNs, invoices)

### Step B: New Vendor Discovery
1. Search online for suppliers matching the PR's product/material specifications
2. For each discovered vendor, collect data following the Discovered Vendor Schema in `context.md` → Section 3
3. Collect as much as possible: company name, website, contact, products, pricing, certifications, delivery terms
4. For any field not found, leave it as `null` and note it in `missingFields`
5. Record the source URL or search description in `discoveredFrom`

## Business Rules

1. Only research vendors for PRs with `status: "approved"`
2. Do not create duplicate research — check if RFx already exists for this PR
3. **Always search for new vendors** — do not skip this step even if existing vendors seem sufficient
4. Target at least 2-3 new vendors per sourcing round
5. Never include blacklisted vendors in the candidate list
6. New vendors with incomplete data are acceptable — mark gaps clearly for the next step

## Output Format

### JSON Output

**1. PR Summary:**

```json
{
  "prNumber": "PR-YYYY-NNNN",
  "category": "...",
  "lineItems": [{ "itemName": "...", "specification": "...", "quantity": 0, "unit": "..." }],
  "budgetAmount": 0,
  "currency": "THB",
  "requiredDate": "YYYY-MM-DD"
}
```

**2. Existing Vendors** — array of candidates from vendor master:

```json
[
  {
    "vendorId": "VND-XXX",
    "vendorName": "...",
    "source": "existing",
    "status": "active",
    "categories": [],
    "certifications": [],
    "riskScore": 0.0,
    "hasHistoricalData": true,
    "contactEmail": "...",
    "contactPhone": "..."
  }
]
```

**3. Discovered Vendors** — array of new vendors found online:

```json
[
  {
    "vendorName": "...",
    "website": "...",
    "contactEmail": "...",
    "contactPhone": "...",
    "source": "discovered",
    "status": "pending",
    "discoveredFrom": "URL or search description",
    "categories": [],
    "certifications": [],
    "availableData": {
      "pricing": true,
      "certifications": false,
      "companyProfile": true,
      "deliveryTerms": false
    },
    "missingFields": ["certifications", "deliveryTerms", "bankAccount"],
    "outreachEmailPlanned": false,
    "outreachStatus": "not_started",
    "outreachRound": 0,
    "dataComplete": false
  }
]
```

### Summary Report

- **PR Overview** — what we're buying, budget, timeline
- **Existing Vendor Shortlist** — which vendors matched, why (categories, certifications, risk scores)
- **Discovered Vendors** — new vendors found, source URLs, what data is available vs missing
- **Data Completeness Overview** — table showing each vendor and % of data collected
- **Next Step** — pass this output to `02a-email-preparation.skill.md` for gap analysis and email drafting

## Chaining

Output feeds into → `02a-email-preparation.skill.md`

The email preparation step will:
- Analyze gaps in discovered vendor data
- Draft outreach emails for vendors with missing data
- Build the unified candidate list
- Create the RFx document

Next: run `02a-email-preparation.skill.md` with this research output.
