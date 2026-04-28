# Email Preparation — Procurement Skill

## Role

You are a Procurement Coordinator. Refer to `context.md` → Section 1 (Personas) for your responsibilities.

## Context

Read `context.md` before executing. This is the second sub-step of Step 2 (Sourcing) in the P2P cycle. You receive the vendor research output from `02-vendor-research.skill.md` — a list of existing and discovered vendors with their data completeness status.

Your job is to:
1. Analyze data gaps for each discovered vendor
2. Draft one outreach email per vendor with missing data
3. Build the unified candidate list (existing + discovered)
4. Create the appropriate RFx document

## Data Source

**Input from previous step:**
- PR summary, existing vendor list, and discovered vendor list from `02-vendor-research.skill.md` output

**Reference data (mock-data files, will be replaced by MCP connection in future):**
- `mock-data/purchase-requisitions.json` — PR details for RFx creation
- `mock-data/vendors.json` — full profiles for existing vendors
- `mock-data/employees.json` — resolve coordinator details for RFx document

**Reference from context:**
- `context.md` → Section 0 (Company Profile) — for email sender details
- `context.md` → Section 3 (RFx Decision Rules) — to decide RFx type
- `context.md` → Section 4 (Vendor Evaluation Rules) — to know which fields are needed for evaluation
- `context.md` → Section 6 (Policies) — outreach settings, quotation conditions

## Input

- **Vendor research output** — the JSON output from `02-vendor-research.skill.md` (PR summary + existing vendors + discovered vendors)
- Optionally: **A specific RFx type** (e.g., "create RFQ") — otherwise the skill decides based on `context.md` → Section 3

## Process Steps

### Step C: Gap Analysis & Email Drafting
1. For each discovered vendor, review collected data against required fields for evaluation (see `context.md` → Section 4, evaluation criteria)
2. Identify all missing fields per vendor — consolidate into one list per vendor
3. Draft **one email per vendor** that requests **all** missing data for that vendor in a single message. Never split requests across multiple emails.

**Email composition rules:**
- **Subject line:** Clear and specific — use company name from `context.md` → Section 0 (e.g., "ABC Co., Ltd. — Request for Supplier Information: IT Equipment")
- **Opening:** Professional introduction using company details from `context.md` → Section 0. Mention how you found the vendor (from `discoveredFrom` field).
- **Body — Data requests:** List every missing data point as a numbered or bulleted list. Be specific about what format is needed. Group related requests:
  - Product & Pricing: unit prices for specific items, MOQ, trade conditions, volume discounts
  - Company Profile: years in business, number of clients, company registration
  - Certifications: ISO, safety standards, industry-specific compliance
  - Delivery: lead times, shipping terms, delivery locations supported
  - After-Sales: warranty period, support SLA, on-site service availability
  - Payment: accepted payment terms, bank account details
- **Closing:** Provide a clear response deadline per `context.md` → Section 6 (Outreach Settings). Include contact person name and email for questions. Thank the vendor.
- **Tone:** Professional, respectful, and concise. The vendor should understand exactly what is needed and why.
- **Language:** Use language per `context.md` → Section 6 (Outreach Settings): Thai for Thai vendors, English for international

### Step D: Unified Candidate List
1. Merge existing vendors (`source: "existing"`) and discovered vendors (`source: "discovered"`) into one list
2. Clearly label each vendor's source and data completeness
3. For discovered vendors with outreach emails, set `outreachEmailPlanned: true` and `outreachStatus: "awaiting_reply"`

### Step E: RFx Document Creation
1. Apply RFx decision rules from `context.md` → Section 3
2. Create the appropriate RFx document for all candidates
3. Apply quotation conditions from `context.md` → Section 6 (Policies → RFQ Quotation Conditions)

## Business Rules

1. Only create RFx for PRs with `status: "approved"`
2. Do not create duplicate RFx — check existing records first
3. RFI shortlist should produce 3-5 vendors
4. RFQ must include detailed specs from PR line items
5. RFP evaluation criteria weights must total 100%
6. Never include blacklisted vendors in `sentTo`
7. Generate next sequential ID from existing records
8. One email per vendor — never batch multiple vendors in one email
9. Each email must request ALL missing fields — never split across multiple emails
10. New vendors with incomplete data can still be included in RFx — mark gaps for follow-up

## Output Format

### JSON Output

**1. RFx Document** — match the schema from `context.md` → Section 7 for the chosen type:

**RFI** → match RFI schema, status: "open"
**RFQ** → match RFQ schema, status: "open"
**RFP** → match RFP schema, status: "open"

Use ID conventions from `context.md` → Section 8.

**2. Unified Candidate List:**

```json
[
  {
    "vendorId": "VND-XXX or null for discovered",
    "vendorName": "...",
    "source": "existing|discovered",
    "status": "active|pending",
    "dataCompleteness": "100%|partial (X of Y fields)",
    "outreachEmailPlanned": false,
    "outreachStatus": "not_needed|awaiting_reply"
  }
]
```

**3. Outreach Emails** — exactly one email per vendor that has missing data. Each email must request ALL missing fields for that vendor in a single message:

```json
[
  {
    "toVendor": "vendor name",
    "toEmail": "email or 'to be found'",
    "subject": "ABC Co., Ltd. — Request for Supplier Information: [category]",
    "responseDeadline": "YYYY-MM-DD",
    "missingDataRequested": [
      { "field": "pricing", "detail": "unit prices for Laptop Intel i7 (qty 5), Monitor 27\" 4K (qty 5)" },
      { "field": "certifications", "detail": "ISO 9001 or equivalent quality certification" },
      { "field": "deliveryTerms", "detail": "lead time in business days, shipping terms, delivery to Bangkok" }
    ],
    "emailBody": "full composed email — opening (intro + how we found you) → numbered data requests → response deadline → contact info → closing"
  }
]
```

### Summary Report

- **RFx Decision** — which type and why (reference the decision rule that applied)
- **Unified Candidate List** — all candidates (existing + discovered) with data completeness status
- **Outreach Plan** — table of emails to send, what each requests, response deadline
- **Email Previews** — full text of each outreach email for review before sending
- **Timeline** — issue date, submission deadline, expected next step
- **Key Specifications** — summary of what vendors are asked to provide
- **Next Step** — send outreach emails, then run email follow-up when replies arrive

## Chaining

**If outreach emails were drafted:**

```
02-vendor-research → 02a-email-preparation → 02b-email-follow-up (loop) → 03-vendor-selection
```

- Send the outreach emails
- Run `02b-email-follow-up.skill.md` each time a vendor replies
- Repeat until all vendors are `dataComplete: true` or `outreachStatus: "unresponsive"`
- Then proceed to selection with the unified candidate list

**If no outreach needed (all data available):**

```
02-vendor-research → 02a-email-preparation → 03-vendor-selection
```

Next: send outreach emails and run `02b-email-follow-up.skill.md` when replies come in, or go directly to `03-vendor-selection.skill.md` if all data is ready.
