# Step 8: Vendor Measurement

## Overview

Vendor Measurement is the ongoing process of evaluating supplier performance after they have been awarded contracts and begun delivering goods or services. Performance data collected here feeds back into future sourcing decisions — it is the critical **feedback loop** that makes vendor selection smarter over time.

## Actors

- **Procurement Team** — tracks and consolidates performance data
- **Requesting Department** — provides quality and satisfaction feedback
- **Warehouse** — provides delivery and inspection data
- **Finance / AP** — provides invoice accuracy and payment data

## Process Steps

```
Define KPIs → Collect Data → Calculate Scores → Review & Report → Feed Back to Sourcing
```

1. **Define KPIs** — set performance indicators and targets per vendor category
2. **Collect Data** — gather actuals from GRN, invoices, support tickets, and feedback
3. **Calculate Scores** — compute KPI values against targets
4. **Review & Report** — generate performance reports, flag underperformers
5. **Feed Back to Sourcing** — use historical performance as input for future vendor evaluation

## KPI Categories

### Delivery KPIs

| KPI | Formula | Target | Frequency |
|-----|---------|--------|-----------|
| On-Time Delivery (OTD) | Orders delivered on time / Total orders x 100 | >= 95% | Monthly |
| Lead Time Variance | Actual lead time - Promised lead time (average) | < +/- 1 day | Monthly |
| Fill Rate | Items delivered / Items ordered x 100 | >= 98% | Quarterly |

### Quality KPIs

| KPI | Formula | Target | Frequency |
|-----|---------|--------|-----------|
| Defect / Rejection Rate | Items rejected / Total items received x 100 | < 1% | Monthly |
| Return Rate | Orders returned / Total orders x 100 | < 2% | Monthly |
| Warranty Claim Rate | Warranty claims / Total items sold x 100 | < 0.5% | Quarterly |

### Cost KPIs

| KPI | Formula | Target | Frequency |
|-----|---------|--------|-----------|
| Price Variance | (Actual price - Contract price) / Contract price x 100 | < 3% | Quarterly |
| Invoice Accuracy Rate | Correct invoices / Total invoices x 100 | >= 98% | Monthly |
| Cost Savings vs Budget | (Budget - Actual cost) / Budget x 100 | > 0% | Annually |

### Compliance & Risk KPIs

| KPI | Formula | Target | Frequency |
|-----|---------|--------|-----------|
| Compliance Score | Score from checklist: certifications, audit results, SLA adherence | >= 90% | Annually |
| Supplier Response Time | Average time vendor responds to RFx or issues | < 48 hours | Per event |
| Supplier Risk Score | Combined score from financial + operational + compliance risk | < Risk threshold | Quarterly |

## How Performance Data Feeds Back

Historical performance data is the best input for future sourcing decisions:

- **High OTD + Low Defect Rate** — vendor gets higher scores in future evaluations
- **Consistent Price Variance** — flag for contract renegotiation
- **Low Compliance Score** — may trigger removal from approved vendor list
- **Repeated Warranty Claims** — reduce quality score in next vendor selection round

## Data Sources

| Data Point | Source System |
|-----------|-------------|
| Delivery dates and quantities | GRN records |
| Quality inspection results | GRN records, support tickets |
| Invoice accuracy | Finance / AP system |
| Contract prices | Contract / PO records |
| Compliance records | Audit system, vendor portal |
| Response times | RFx system, email logs |

## Related Documents

- Input: Delivery data from [Step 6: Delivery & Receipt](06-delivery-and-receipt.md), Invoice data from [Step 7: Invoice & Payment](07-invoice-and-payment.md)
- Output: Performance scores feed back into [Step 2: Sourcing](02-sourcing.md) and [Step 3: Vendor Selection](03-vendor-selection.md)

## Related Mock Data

- [vendor-scorecards.json](../mock-data/vendor-scorecards.json)
- [vendors.json](../mock-data/vendors.json)
