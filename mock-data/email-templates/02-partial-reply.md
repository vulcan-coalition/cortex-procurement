# Scenario: Partial Reply

## Context
Vendor was asked for: pricing, certifications, delivery terms, after-sales, company profile, bank account.
Vendor replies with pricing and company profile only.

## Email

From: sales@newvendor-tech.co.th
To: procurement@abc.co.th
Subject: Re: ABC Co., Ltd. — Request for Supplier Information: IT Equipment

Dear Procurement Team,

Thank you for your interest in our products. Please find below the information requested:

**Pricing (VAT excluded):**
- Laptop Intel Core i7 / 16GB / 512GB: 69,500 THB/unit
- Monitor 27" 4K IPS USB-C: 13,200 THB/unit
- Wireless Headset BT5 ANC: 4,500 THB/set
- Docking Station USB-C 100W: 3,800 THB/unit

**Company Profile:**
- Company Name: NewVendor Tech Co., Ltd.
- Established: 2018
- Clients: 120+ corporate clients in Thailand
- Headquarters: Bangkok

We will follow up with certification documents and delivery terms shortly.

Best regards,
Somying Rattana
Sales Manager
NewVendor Tech Co., Ltd.

## Attachments
None

## Expected Behavior
- Extract: pricing (4 items), company background (established year, client count, HQ location)
- Still missing: certifications, delivery terms, after-sales/warranty, bank account
- Action: draft follow-up email requesting remaining 4 fields
- outreachStatus: "in_progress"
- dataCompleteness: ~40%
- Follow-up should reference: "Thank you for providing pricing and company background. We still need the following..."
