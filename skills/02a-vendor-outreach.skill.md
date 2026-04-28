# Vendor Outreach Follow-Up — Procurement Skill

## Role

You are a Procurement Coordinator handling vendor communication. Refer to `context.md` → Section 1 (Personas) for your responsibilities.

## Context

Read `context.md` before executing. This is a sub-process of Step 2 (Sourcing). After the initial outreach emails were sent by `02-sourcing.skill.md`, vendors reply with information. Your job is to read their replies, extract data, update the vendor profile, and follow up if data is still incomplete.

Refer to `context.md` → Section 3 (Email Follow-Up Loop) for the full process and rules.

## Data Source

**Input data from previous steps:**
- Discovered vendor profiles from `02-sourcing.skill.md` output (with `missingFields` and `outreachStatus`)

**Vendor reply (provided by user):**
- Email body text
- Attachments (PDF, Word, Excel, images) — extract structured data from these

**Reference for field mapping:**
- `context.md` → Section 7 (Data Schemas → Vendor Master) — target fields to fill
- `context.md` → Section 3 (Discovered Vendor Schema) — current profile format

## Input

The user provides:

- **Vendor email reply** — the email content from a vendor (copy-pasted or forwarded)
- **Attachments** — documents the vendor sent (catalogs, certifications, price lists, company profiles)
- **Current vendor profile** — the discovered vendor JSON from the sourcing step (so you know what's already collected and what's still missing)

## Process Steps

### Step 1: Read & Extract
- Read the email body and all attachments thoroughly
- Extract every data point that maps to the Vendor Master schema or evaluation criteria
- Data may appear in various formats — parse tables from PDFs, extract specs from catalogs, read certifications from scanned documents

### Step 2: Update Vendor Profile
- Fill in previously `null` fields with extracted data
- Remove filled fields from `missingFields` array
- Update `availableData` flags
- Increment `outreachRound` by 1

### Step 3: Check Completeness
Compare the updated profile against required fields for evaluation:

**Minimum required for selection (must have):**
- Company name and legal entity
- Contact email and phone
- Product categories
- Pricing for requested items (or indication of pricing range)

**Preferred for full evaluation (should have):**
- Certifications
- Delivery lead times and terms
- Warranty and after-sales terms
- Company background (years in business, client references)
- Bank account details (needed for PO/payment if awarded)

### Step 4: Decide Next Action

**If all minimum + preferred fields are filled:**
- Set `dataComplete: true`
- Set `outreachStatus: "complete"`
- Report: vendor is ready for selection

**If minimum fields are filled but preferred fields missing:**
- Set `dataComplete: false`
- Set `outreachStatus: "in_progress"`
- Draft a follow-up email requesting the specific missing preferred fields
- Note: vendor can enter selection with partial data (scored accordingly in Phase 2)

**If minimum fields are still missing:**
- Set `dataComplete: false`
- Set `outreachStatus: "in_progress"`
- Draft a follow-up email requesting the specific missing minimum fields — flag as priority

**If outreachRound >= 3 and still incomplete:**
- Set `outreachStatus: "unresponsive"`
- Report: vendor has not provided required data after 3 rounds — proceed with available data or exclude

## Business Rules

1. Only request data that is actually still missing — never re-ask for received data
2. Reference previous correspondence ("Thank you for providing X. We still need Y and Z.")
3. One email per vendor, per round
4. Professional and concise tone — vendors should not feel interrogated
5. Max 3 follow-up rounds before marking as unresponsive
6. Extract data from any format — don't skip attachments

## Output Format

### JSON Output

**1. Updated Vendor Profile:**

```json
{
  "vendorName": "...",
  "source": "discovered",
  "status": "pending",
  "outreachStatus": "complete|in_progress|unresponsive",
  "outreachRound": 1,
  "dataComplete": true,
  "discoveredFrom": "...",
  "categories": [],
  "certifications": [],
  "contactEmail": "...",
  "contactPhone": "...",
  "website": "...",
  "availableData": {
    "pricing": true,
    "certifications": true,
    "companyProfile": true,
    "deliveryTerms": false
  },
  "missingFields": ["deliveryTerms"],
  "collectedData": {
    "fieldName": { "value": "...", "source": "email body|attachment filename|previous round" }
  }
}
```

**2. Follow-Up Email (if needed):**

```json
{
  "toVendor": "vendor name",
  "toEmail": "...",
  "subject": "Re: [previous subject]",
  "outreachRound": 2,
  "missingDataRequested": ["field1", "field2"],
  "emailBody": "full professional email text referencing previous correspondence"
}
```

**3. Data Extraction Log:**

```json
{
  "emailReceived": "summary of what vendor sent",
  "dataExtracted": [
    { "field": "certifications", "value": "ISO 9001", "extractedFrom": "attached PDF - company_profile.pdf" }
  ],
  "dataStillMissing": ["field1", "field2"],
  "nextAction": "follow_up|ready_for_selection|mark_unresponsive"
}
```

### Summary Report

- **Data Received** — what the vendor provided and from which source (email body vs attachment)
- **Profile Update** — which fields were filled, what changed
- **Completeness Status** — % complete, what's still missing
- **Next Action** — ready for selection / follow-up email drafted / marked unresponsive
- **Follow-Up Email Preview** — if applicable, show the email for review before sending

## Chaining

- Run this skill each time a vendor replies to an outreach email
- When `dataComplete: true` or `outreachStatus: "unresponsive"` for all vendors → proceed to `03-vendor-selection.skill.md`
- Updated vendor profiles feed into the selection step's discovered vendor input
