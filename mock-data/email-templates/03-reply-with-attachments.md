# Scenario: Reply with Mixed Sources (Email Body + Attachments)

## Context
Vendor was asked for: pricing, certifications, delivery terms, after-sales, company profile, bank account.
Vendor provides some data in email body and the rest in attachments.

## Email

From: contact@bangkokit.co.th
To: procurement@abc.co.th
Subject: Re: ABC Co., Ltd. — Request for Supplier Information: IT Equipment

Dear ABC Co., Ltd.,

Thank you for considering us. Here is our preliminary information:

**Delivery:**
- Standard lead time: 7-10 business days within Bangkok
- We use Kerry Express for all deliveries
- Free delivery for orders above 100,000 THB

**After-Sales:**
- All products carry manufacturer warranty
- We provide additional 1-year extended warranty on all items
- Support available Mon-Fri 09:00-18:00

Please see the attached files for our company profile, pricing, and certification.

Kind regards,
Pimchanok Sae-lim
BangkokIT Solutions Co., Ltd.
Tel: 02-333-4444

## Attachments

### Attachment 1: BangkokIT_Company_Profile.pdf

BangkokIT Solutions Co., Ltd.
Registration: 0105560078901
Address: 45 Rama 3 Road, Yannawa, Bangkok 10120
Founded: 2017
Employees: 60
Specialization: IT Equipment, Networking, Cloud Solutions
Key Clients: Siam Commercial Bank, CP Group, Bumrungrad Hospital

Certifications:
- ISO 9001:2015 (valid until 2027-03-15)
- Microsoft Authorized Reseller
- HP Platinum Partner

### Attachment 2: Price_Quote_ABC.xlsx

| Item | Brand/Model | Unit Price (THB) | Availability |
|------|------------|-----------------|-------------|
| Laptop i7 16GB 512GB | HP ProBook 450 G10 | 70,200 | In stock |
| Monitor 27" 4K USB-C | Dell U2723QE | 14,100 | In stock |
| Wireless Headset BT ANC | Jabra Evolve2 75 | 4,900 | 2-week backorder |
| Docking Station USB-C | HP USB-C Dock G5 | 4,100 | In stock |

Note: Prices exclude VAT 7%. Valid for 30 days.

## Expected Behavior
- Extract from email body: delivery terms (lead time, carrier, free delivery threshold), after-sales (warranty, support hours)
- Extract from PDF: company profile (name, registration, address, founded, employees, clients), certifications (ISO 9001, MS Reseller, HP Partner)
- Extract from Excel: pricing (4 items with brand/model), availability status
- Still missing: bank account, payment terms
- Action: draft follow-up requesting bank account and payment terms
- outreachStatus: "in_progress"
- dataCompleteness: ~80%
