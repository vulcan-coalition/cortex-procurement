# Scenario: Complete Reply

## Context
Vendor was asked for: pricing, certifications, delivery terms, after-sales, company profile, bank account.
Vendor replies with ALL requested information in one email.

## Email

From: sales@alphatech.co.th
To: procurement@abc.co.th
Subject: Re: ABC Co., Ltd. — Request for Supplier Information: IT Equipment

Dear ABC Co., Ltd. Procurement Team,

Thank you for reaching out. We are pleased to provide the following information as requested.

**Company Profile:**
- Legal Name: AlphaTech Solutions Co., Ltd.
- Registration No: 0105558034567
- Address: 199 Phahonyothin Road, Chatuchak, Bangkok 10900
- Established: 2012
- Employees: 150+
- Key Clients: Kasikorn Bank, AIS, Central Group, True Corporation
- Website: www.alphatech.co.th

**Certifications:**
- ISO 9001:2015 (Quality Management)
- ISO 14001:2015 (Environmental Management)
- BOI Promoted Company

**Pricing (VAT excluded):**
- Laptop Intel Core i7 / 16GB DDR5 / 512GB NVMe SSD: 68,500 THB/unit
- Monitor 27" 4K IPS USB-C Hub: 12,900 THB/unit
- Wireless Headset BT5.3 ANC: 4,200 THB/set
- Docking Station USB-C 100W HDMI×2: 3,600 THB/unit

Volume discount: 5% for orders above 500,000 THB

**Delivery Terms:**
- Lead time: 10-14 business days after PO confirmation
- Delivery to Bangkok: free of charge
- Delivery outside Bangkok: additional shipping cost quoted separately
- Shipping via our own logistics fleet

**After-Sales & Warranty:**
- Laptop & Monitor: 3-year on-site warranty, next business day response
- Headset & Docking Station: 1-year carry-in warranty
- Dedicated support hotline: 02-999-8888 (Mon-Fri, 08:30-17:30)
- SLA: response within 4 hours, resolution within 24 hours

**Payment Terms:**
- Net 30 days after delivery and GRN
- Accept bank transfer

**Bank Account:**
- Bank: Bangkok Bank
- Branch: Chatuchak
- Account Number: 678-9-01234-5
- Account Name: AlphaTech Solutions Co., Ltd.

Please do not hesitate to contact us if you need any additional information.

Best regards,
Wichai Tanaka
Sales Director
AlphaTech Solutions Co., Ltd.
Tel: 02-999-8888
Email: sales@alphatech.co.th

## Attachments
None

## Expected Behavior
- Extract: ALL fields — pricing (4 items + volume discount), certifications (3), delivery terms, after-sales/warranty, payment terms, bank account, company profile
- Missing fields: none
- Action: mark vendor as dataComplete: true
- outreachStatus: "complete"
- dataCompleteness: 100%
- No follow-up email needed
