# Step 7: Invoice & Payment

## Overview

The vendor submits a **Tax Invoice** to request payment. Finance/AP verifies the invoice against the PO and GRN through **3-Way Matching**. If all three documents match, payment is approved according to the agreed terms.

## Actors

- **Vendor** — issues the tax invoice
- **Finance / AP (Accounts Payable)** — receives, verifies, and processes payment
- **Procurement Team** — resolves discrepancies between PO, GRN, and Invoice
- **Payment Approver** — authorizes the payment

## Process Steps

```
Vendor Submits Invoice → AP Receives → 3-Way Match (PO + GRN + Invoice) → Resolve Discrepancies → Approve Payment → Execute Payment
```

1. **Vendor Submits Invoice** — vendor sends tax invoice referencing the PO number
2. **AP Receives** — finance records the invoice in the AP system
3. **3-Way Match** — verify invoice line items, quantities, and amounts against PO and GRN
4. **Resolve Discrepancies** — if mismatch found, coordinate with procurement and vendor
5. **Approve Payment** — once matched, payment is approved
6. **Execute Payment** — payment is made per agreed terms (e.g., Net 30 days)

## Tax Invoice Document

### Header Fields

| Field | Description |
|-------|------------|
| Invoice Number | Vendor's invoice number (e.g., INV-TP-2024-8821) |
| Issuer | Vendor name, address, tax ID |
| Issued To | Buyer organization name, address, tax ID |
| Invoice Date | Date the invoice was issued |
| PO Reference | PO number and GRN number |
| Payment Due Date | Calculated from payment terms (e.g., Net 30 days) |

### Line Items Structure

| Field | Description |
|-------|------------|
| Item Number | Sequential number |
| Item Name | Product/service description |
| Quantity | Invoiced quantity |
| Unit | Unit of measure |
| Unit Price | Price per unit |
| Total | Quantity x unit price |

### Totals

| Field | Description |
|-------|------------|
| Subtotal (before VAT) | Sum of all line items |
| VAT (7%) | Calculated tax |
| Grand Total | Subtotal + VAT |

### Handling Partial Deliveries

When not all items were delivered (e.g., 4 of 5 Docking Stations received), the invoice may cover only delivered items. A separate invoice is issued after the remaining items are delivered.

### Payment Information

| Field | Description |
|-------|------------|
| Bank | Vendor's bank name and branch |
| Account Number | Bank account number |
| Account Name | Registered account name |
| Remittance | Where to send payment confirmation |

### 3-Way Match Verification

| Check | What is Compared |
|-------|-----------------|
| PO vs Invoice | Items, quantities, and prices match the PO |
| GRN vs Invoice | Invoiced quantities match what was actually received |
| PO vs GRN | Already matched during receipt |

All three must match before payment is approved. AP processing proceeds after successful match.

### Signatures

| Role | Responsibility |
|------|---------------|
| Invoice Issuer (Vendor) | Certifies the invoice |
| AP Receiver (Finance) | Confirms receipt and match |
| Payment Approver | Authorizes fund release |

## Related Documents

- Input: GRN from [Step 6: Delivery & Receipt](06-delivery-and-receipt.md), PO from [Step 5: Purchase Order](05-purchase-order.md)
- Output: Payment data feeds into [Step 8: Vendor Measurement](08-vendor-measurement.md)

## Related Mock Data

- [tax-invoices.json](../mock-data/tax-invoices.json)
