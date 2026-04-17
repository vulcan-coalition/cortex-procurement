# Step 5: Purchase Order

## Overview

A **Purchase Order (PO)** is the formal, legally binding document issued to the selected vendor. It specifies exactly what is being ordered, at what price, and under what delivery and payment terms. The PO is a key document in the 3-Way Matching process (PO + GRN + Invoice).

## Actors

- **Procurement Team** — creates and issues the PO
- **Vendor** — receives and acknowledges the PO
- **Approver** — authorizes the PO before it is sent

## Process Steps

```
Create PO → Approval → Send to Vendor → Vendor Acknowledges → Track Delivery
```

1. **Create PO** — procurement drafts the PO referencing the contract and PR
2. **Approval** — PO is approved internally
3. **Send to Vendor** — PO is officially sent to the vendor
4. **Vendor Acknowledges** — vendor confirms receipt and acceptance
5. **Track Delivery** — monitor against delivery deadline

## Purchase Order Document

### Header Fields

| Field | Description |
|-------|------------|
| PO Number | Unique identifier (e.g., PO-2024-1102) |
| Buyer | Organization name, address, tax ID, contact |
| Vendor | Vendor name, address, tax ID, contact |
| PO Date | Date the PO is issued |
| Delivery Deadline | Expected delivery date (e.g., 21 business days) |
| Payment Terms | e.g., Net 30 days after receiving goods and GRN |
| Delivery Location | Where goods should be delivered |

### Line Items Structure

| Field | Description |
|-------|------------|
| Item Number | Sequential number |
| Item Name | Product/service name |
| Specification | Brief spec description |
| Quantity | Ordered quantity |
| Unit | Unit of measure |
| Unit Price | Agreed price per unit |
| Total | Quantity x unit price |

### Totals

| Field | Description |
|-------|------------|
| Subtotal (before VAT) | Sum of all line item totals |
| VAT (7%) | Calculated tax amount |
| Grand Total | Subtotal + VAT |

### Special Conditions

Example conditions from a real PO:
- Price includes VAT, shipping, and installation
- Products must have warranty with on-site next business day service
- Late delivery penalty: 0.1% per day

### Signatures

| Role | Responsibility |
|------|---------------|
| PO Receiver (Vendor) | Acknowledges the order |
| PO Issuer (Procurement) | Confirms the order |
| Approver | Authorizes the purchase |

## Related Documents

- Input: Contract from [Step 4: Contract & Negotiation](04-contract-and-negotiation.md)
- Output: PO is matched against GRN in [Step 6: Delivery & Receipt](06-delivery-and-receipt.md)

## Related Mock Data

- [purchase-orders.json](../mock-data/purchase-orders.json)
