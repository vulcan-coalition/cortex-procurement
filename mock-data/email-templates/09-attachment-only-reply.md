# Scenario: Attachment-Only Reply (Minimal Email Body)

## Context
Vendor was asked for: pricing, certifications, delivery terms, company profile.
Vendor replies with a brief email and attaches everything in files — no detail in the email body itself.

## Email

From: info@siamdigital.co.th
To: procurement@abc.co.th
Subject: Re: ABC Co., Ltd. — Request for Supplier Information: IT Equipment

Dear Sir/Madam,

Please find the attached documents as requested.

Best regards,
Kannika Sripong
Siam Digital Supply Co., Ltd.

## Attachments

### Attachment 1: Company_Profile_SiamDigital.pdf

Siam Digital Supply Co., Ltd.
Registration No: 0105561012345
Address: 88 Bangna-Trad Road, Bangna, Bangkok 10260
Established: 2015
Employees: 85
Key Clients: Government Savings Bank, PTT, Minor International
ISO 9001:2015 Certified (Certificate No: TH-QMS-2023-0892)
ISO 27001:2022 Certified (Certificate No: TH-ISMS-2024-0156)

### Attachment 2: Quotation_IT_Equipment_2026.xlsx

| Item | Specification | Unit Price (THB) | MOQ | Lead Time |
|------|--------------|-----------------|-----|-----------|
| Laptop | Intel i7-1365U / 16GB DDR5 / 512GB NVMe | 71,000 | 1 | 14 business days |
| Monitor 27" | 4K IPS, USB-C 65W, HDMI×2 | 13,800 | 1 | 10 business days |
| Wireless Headset | BT 5.3, ANC, 35hr battery | 4,650 | 5 | 7 business days |
| Docking Station | USB-C 100W, HDMI×2, RJ45, SD | 3,950 | 1 | 7 business days |

Payment Terms: Net 30
Warranty: 3 years on-site for Laptop/Monitor, 1 year for accessories
Quotation Valid Until: 2026-06-30

### Attachment 3: ISO_9001_Certificate.jpg

[Scanned image of ISO 9001:2015 certificate issued by TÜV SÜD, valid until 2026-12-31]

## Expected Behavior
- Email body contains almost nothing — agent must extract ALL data from attachments
- From PDF: company name, registration, address, established year, employees, key clients, certifications (ISO 9001 + ISO 27001)
- From Excel: pricing (4 items), MOQ, lead times, payment terms, warranty terms
- From Image: verify ISO 9001 certificate validity
- Still missing: bank account details
- Action: draft follow-up requesting only bank account
- outreachStatus: "in_progress"
- dataCompleteness: ~90% (only bank account missing)
