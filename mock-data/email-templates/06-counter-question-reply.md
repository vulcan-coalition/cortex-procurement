# Scenario: Counter-Question Reply

## Context
Vendor was asked for: pricing, certifications, delivery terms, after-sales, company profile, bank account.
Vendor asks clarifying questions instead of providing the requested data.

## Email

From: sales@precisionit.co.th
To: procurement@abc.co.th
Subject: Re: ABC Co., Ltd. — Request for Supplier Information: IT Equipment

Dear ABC Co., Ltd. Procurement Team,

Thank you for your inquiry. Before we can provide a formal quotation, we would like to clarify a few points:

1. **Laptop specification:** Do you require Intel i7 13th Gen or 14th Gen? We have different pricing for each. Also, do you need a specific brand (HP, Dell, Lenovo) or is any brand acceptable?

2. **Monitor:** Do you need a built-in USB-C hub with power delivery, or is a standard USB-C input sufficient? This significantly affects pricing.

3. **Quantity:** Your request mentions 5 laptops and 5 monitors. Is this the final quantity, or is there potential for a larger order? We offer tiered pricing for bulk orders.

4. **Delivery timeline:** Is the required date firm, or is there flexibility? We may be able to offer better pricing with a longer lead time.

5. **Contract type:** Are you looking for a one-time purchase or a framework agreement for recurring IT equipment needs?

We want to make sure our quotation is accurate and competitive. Please advise, and we will respond within 2 business days.

Best regards,
Natthapong Chairat
Key Account Manager
PrecisionIT Co., Ltd.
Tel: 081-234-5678
Email: natthapong@precisionit.co.th

## Attachments
None

## Expected Behavior
- Extract: contact person (name, phone, email), company name, vendor shows professional sales process
- NOT extractable: pricing, certifications, delivery terms, after-sales, bank account — vendor is asking questions instead
- Still missing: all originally requested fields
- Action: draft a reply that ANSWERS the vendor's questions using data from the PR (specs, quantities, timeline) AND re-requests the missing data. This is a two-part email:
  1. Answer their 5 questions based on PR details
  2. Re-state the data we still need (certifications, company profile, bank account, etc.)
- outreachStatus: "in_progress"
- dataCompleteness: ~5%
- Flag: vendor is engaged and professional but needs clarification before providing data — this is a positive signal, not a problem
