# Scenario: Pricing Only Reply

## Context
Vendor was asked for: pricing, certifications, delivery terms, after-sales, company profile, bank account.
Vendor only sends a price list and ignores all other requests.

## Email

From: quotation@fastpc.co.th
To: procurement@abc.co.th
Subject: Re: ABC Co., Ltd. — Request for Supplier Information: IT Equipment

Hi,

Please see our prices below:

Laptop i7/16GB/512GB - 73,000 baht
Monitor 27 4K - 15,500 baht
Headset bluetooth - 5,200 baht
Docking USB-C - 4,500 baht

All prices before VAT. Minimum order 3 units per item.

Thanks,
FastPC

## Attachments
None

## Expected Behavior
- Extract: pricing (4 items), MOQ (3 units per item)
- Still missing: certifications, delivery terms, after-sales/warranty, company profile, bank account, payment terms
- Action: draft follow-up requesting ALL remaining fields — this is a significant gap
- Note: vendor's email is informal and brief — follow-up should still be professional
- outreachStatus: "in_progress"
- dataCompleteness: ~20%
- Flag: vendor did not address most of the original request
