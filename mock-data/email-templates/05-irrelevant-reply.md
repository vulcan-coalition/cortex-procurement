# Scenario: Irrelevant Reply

## Context
Vendor was asked for: pricing, certifications, delivery terms, after-sales, company profile, bank account.
Vendor replies but with generic marketing content that doesn't answer the specific questions.

## Email

From: marketing@megasupply.co.th
To: procurement@abc.co.th
Subject: Re: ABC Co., Ltd. — Request for Supplier Information: IT Equipment

Dear Valued Customer,

Thank you for your email! MegaSupply is Thailand's leading IT distributor with over 20 years of experience serving enterprises across Southeast Asia.

We offer a comprehensive range of products from leading brands including Dell, HP, Lenovo, Apple, Samsung, and many more. Our dedicated team of IT specialists is ready to help you find the perfect solution for your needs.

Please visit our website at www.megasupply.co.th to browse our full catalog. You can also visit our showroom at CentralWorld, 5th Floor, for a hands-on experience.

We look forward to serving you!

Warm regards,
MegaSupply Marketing Team
Tel: 1800-MEGA-SUPPLY
www.megasupply.co.th

## Attachments

### Attachment 1: MegaSupply_Brochure_2026.pdf

[Generic marketing brochure with product category images, corporate logos, and taglines. No specific pricing, no certifications listed, no delivery terms.]

## Expected Behavior
- Extract: company name, website, showroom location, years in business ("over 20 years"), product categories (IT Equipment — Dell, HP, Lenovo, etc.)
- NOT extractable: pricing, certifications, delivery terms, after-sales, bank account, payment terms — none of the requested data was provided
- Still missing: pricing, certifications, delivery terms, after-sales, bank account
- Action: draft follow-up that politely re-states the specific data needed, referencing the original request. Be explicit that generic information is not sufficient.
- outreachStatus: "in_progress"
- dataCompleteness: ~10%
- Flag: vendor responded with marketing material instead of requested data
