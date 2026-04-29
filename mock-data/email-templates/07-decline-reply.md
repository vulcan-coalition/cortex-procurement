# Scenario: Decline to Participate

## Context
Vendor was asked for: pricing, certifications, delivery terms, after-sales, company profile, bank account.
Vendor declines to participate in the sourcing process.

## Email

From: bd@eliteoffice.co.th
To: procurement@abc.co.th
Subject: Re: ABC Co., Ltd. — Request for Supplier Information: IT Equipment

Dear ABC Co., Ltd.,

Thank you for considering Elite Office Co., Ltd. for your IT equipment sourcing.

After reviewing your requirements, we regret to inform you that we are unable to participate in this sourcing round for the following reasons:

1. We are currently at full capacity with existing contracts and cannot commit to new deliveries within your required timeline.
2. The product specifications you require (Intel i7 laptops, 4K monitors) are not within our standard inventory — we primarily supply office furniture and peripherals, not core IT hardware.

We would be happy to be considered for future sourcing rounds, particularly for office equipment, peripherals, and accessories.

Thank you for your understanding.

Best regards,
Arisa Wongsawat
Business Development Manager
Elite Office Co., Ltd.
Tel: 02-555-6666

## Attachments
None

## Expected Behavior
- Extract: vendor declines, reasons (capacity + category mismatch)
- Action: NO follow-up email needed
- outreachStatus: "declined" (or remove from candidate list)
- dataComplete: false
- Recommendation: remove from unified candidate list for this sourcing round. Note the category mismatch — this vendor may have been incorrectly matched during discovery.
- Flag: vendor is willing to participate in future rounds for office equipment — note for future reference
