# Vendor Research — Procurement Skill

## Role

You are a Procurement Coordinator. Refer to `context.md` → Section 1 (Personas) for your responsibilities.

## Context

Read `context.md` before executing. This is the first sub-step of Step 2 (Sourcing) in the P2P cycle. An approved PR triggers this step. Your job is to:

1. Research and compile vendor candidates (existing + online discovery)
2. Analyze data gaps for each discovered vendor
3. Build the unified candidate list
4. Create the appropriate RFx document

**Critical:** You must not only look at existing vendors. Every sourcing round requires searching for new alternative vendors online. Refer to `context.md` → Section 3 (Alternative Sourcing) for the full process.

Your output feeds into `02a-email-preparation.skill.md` for email drafting (vendors with missing data) and into `03-vendor-selection.skill.md` (when all data is ready).

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
- Optionally: **A specific RFx type** (e.g., "create RFQ") — otherwise the skill decides based on `context.md` → Section 3

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

### Step C: Gap Analysis
1. For each discovered vendor, review collected data against required fields for evaluation (see `context.md` → Section 4, evaluation criteria)
2. Identify all missing fields per vendor — consolidate into one list per vendor
3. Determine which vendors need outreach emails and what data each email should request
4. Set `outreachEmailPlanned: true` for vendors with missing data

### Step D: Unified Candidate List
1. Merge existing vendors (`source: "existing"`) and discovered vendors (`source: "discovered"`) into one list
2. Clearly label each vendor's source and data completeness
3. For discovered vendors needing outreach, set `outreachStatus: "awaiting_reply"`

### Step E: RFx Document Creation
1. Apply RFx decision rules from `context.md` → Section 3
2. Create the appropriate RFx document for all candidates
3. Apply quotation conditions from `context.md` → Section 6 (Policies → RFQ Quotation Conditions)
4. Generate next sequential ID by reading existing records
5. Use ID conventions from `context.md` → Section 8

## Business Rules

1. Only research vendors for PRs with `status: "approved"`
2. Do not create duplicate RFx — check if one already exists for this PR
3. **Always search for new vendors** — do not skip this step even if existing vendors seem sufficient
4. Target at least 2-3 new vendors per sourcing round
5. Never include blacklisted vendors in the candidate list
6. New vendors with incomplete data are acceptable — mark gaps clearly
7. Every collected data point for discovered vendors must include confidence, source, and justification — see `context.md` → Section 3 (Data Confidence Rules)
8. If no specific source can be cited for a data point, set the value to `null` — never guess or hallucinate
9. RFI shortlist should produce 3-5 vendors
10. RFQ must include detailed specs from PR line items
11. RFP evaluation criteria weights must total 100%
12. Never include blacklisted vendors in `sentTo`

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

**2. Unified Candidate List:**

```json
[
  {
    "vendorId": "VND-XXX or null for discovered",
    "vendorName": "...",
    "source": "existing|discovered",
    "status": "active|pending",
    "categories": [],
    "certifications": [],
    "riskScore": 0.0,
    "contactEmail": "...",
    "contactPhone": "...",
    "website": "...",
    "discoveredFrom": "URL or null for existing",
    "hasHistoricalData": true,
    "dataCompleteness": "100%|partial (X of Y fields)",
    "availableData": {
      "pricing": true,
      "certifications": false,
      "companyProfile": true,
      "deliveryTerms": false
    },
    "missingFields": ["certifications", "deliveryTerms"],
    "outreachEmailPlanned": true,
    "outreachStatus": "not_needed|awaiting_reply",
    "outreachRound": 0,
    "dataComplete": true,
    "collectedData": {
      "pricing": {
        "value": "72,000 THB/unit for Laptop",
        "confidence": 0.5,
        "source": "https://vendor-website.com/products/laptop-i7",
        "justification": "Price listed on product page but may be consumer retail price, not B2B"
      },
      "companyProfile": {
        "value": "Established 2015, 80 employees",
        "confidence": 0.8,
        "source": "https://vendor-website.com/about",
        "justification": "From vendor's official About page"
      }
    }
  }
]
```

**3. RFx Document** — match the schema from `context.md` → Section 7 for the chosen type:

**RFI** → match RFI schema, status: "open"
**RFQ** → match RFQ schema, status: "open"
**RFP** → match RFP schema, status: "open"

**4. Email Preparation Input** — for each vendor needing outreach, provide a structured input for the email drafting service:

```json
[
  {
    "vendorName": "...",
    "contactEmail": "...",
    "discoveredFrom": "URL or search description",
    "category": "...",
    "missingFields": [
      { "field": "pricing", "detail": "unit prices for Laptop Intel i7 (qty 5), Monitor 27\" 4K (qty 5)" },
      { "field": "certifications", "detail": "ISO 9001 or equivalent quality certification" },
      { "field": "deliveryTerms", "detail": "lead time in business days, shipping terms, delivery to Bangkok" }
    ]
  }
]
```

### Summary Report

- **PR Overview** — what we're buying, budget, timeline
- **RFx Decision** — which type and why (reference the decision rule that applied)
- **Existing Vendor Shortlist** — which vendors matched, why (categories, certifications, risk scores)
- **Discovered Vendors** — new vendors found, source URLs, what data is available vs missing
- **Gap Analysis** — table showing each vendor, data completeness %, and what's missing
- **Unified Candidate List** — all candidates with source label and completeness status
- **RFx Document** — the created RFx with timeline
- **Next Step** — pass email preparation input to `02a-email-preparation.skill.md` for vendors with missing data, or go directly to `03-vendor-selection.skill.md` if all data is ready

## Chaining

**If vendors have missing data:**

```
02-vendor-research → 02a-email-preparation → [02b-email-extraction → 02c-email-follow-up-draft] (loop) → 03-vendor-selection
```

- Pass the Email Preparation Input to `02a-email-preparation.skill.md` for email drafting
- After emails are sent, run `02b-email-extraction.skill.md` for reply processing

**If all data is available:**

```
02-vendor-research → 03-vendor-selection
```

Next: run `02a-email-preparation.skill.md` with the email preparation input, or `03-vendor-selection.skill.md` directly if no outreach is needed.
