# Step 6: Delivery & Receipt

## Overview

When the vendor delivers goods, the warehouse inspects them against the PO for quantity, quality, and condition. A **Goods Receipt Note (GRN)** is created to document what was received. The GRN is a critical document in the **3-Way Matching** process (PO + GRN + Invoice).

## Actors

- **Warehouse Staff** — receives and inspects goods physically
- **Requesting Department (e.g., IT)** — verifies technical quality / functionality
- **Inventory Manager** — records receipt in the inventory system

## Process Steps

```
Vendor Delivers → Warehouse Receives → Inspect Quantity & Quality → Record GRN → Flag Discrepancies → 3-Way Match Status
```

1. **Vendor Delivers** — goods arrive at the designated delivery location
2. **Warehouse Receives** — warehouse staff checks shipment against PO
3. **Inspect Quantity & Quality** — verify item count, condition, and spec compliance
4. **Record GRN** — create GRN document with inspection results
5. **Flag Discrepancies** — note any shortages, damages, or quality issues
6. **3-Way Match Status** — update matching status (PO + GRN, waiting for Invoice)

## Goods Receipt Note (GRN) Document

### Header Fields

| Field | Description |
|-------|------------|
| GRN Number | Unique identifier (e.g., GRN-2024-0521) |
| PO Reference | The PO this delivery fulfills (e.g., PO-2024-1102) |
| Vendor | Supplier name |
| Receipt Date | Date and time goods were received |
| Received By | Person who accepted delivery (name and role) |
| Receipt Location | Warehouse location (e.g., Warehouse Floor 1, Zone B) |

### Inspection Line Items

| Field | Description |
|-------|------------|
| Item Number | Sequential number |
| Item Name | Product name |
| Ordered (PO) | Quantity as stated in PO |
| Received | Actual quantity received |
| Rejected | Quantity that failed inspection |
| Condition | Normal / Partial / Damaged |
| Remarks | Inspection notes (e.g., "Seal intact", "Box has scratches") |

### 3-Way Matching Status

The GRN tracks matching status against PO and Invoice:

| Document | Status |
|----------|--------|
| PO | Match / Mismatch |
| GRN | Received (count of items, any pending resolution) |
| Invoice | Waiting / Received / Matched |

### Handling Discrepancies

When received goods don't match the PO:
- **Shortage** — fewer items received than ordered; vendor must ship remainder
- **Damage** — items received in poor condition; vendor arranges replacement
- **Partial delivery** — some items pending; GRN records partial receipt with a note

Example: 1 Docking Station received with damaged box, under investigation. Vendor to send replacement within 3 business days.

### Signatures

| Role | Responsibility |
|------|---------------|
| Warehouse Staff | Confirms physical receipt |
| Requesting Department (e.g., IT) | Verifies functional quality |
| Inventory Manager | Records in inventory system |

## Related Documents

- Input: PO from [Step 5: Purchase Order](05-purchase-order.md)
- Output: GRN feeds into [Step 7: Invoice & Payment](07-invoice-and-payment.md) for 3-Way Matching

## Related Mock Data

- [goods-receipt-notes.json](../mock-data/goods-receipt-notes.json)
