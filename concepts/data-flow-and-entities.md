# Data Flow and Entities

## Key Systems

| System | Examples | Core Data | Role |
|--------|----------|-----------|------|
| ERP | SAP, Oracle, Microsoft Dynamics | Vendor Master, PO, GRN, Invoice, Budget | Core system of record |
| e-Procurement Platform | Coupa, Jaggaer, Ariba | RFx, Bid, Contract, Approval Workflow | Sourcing & contracting hub |
| Supplier Portal | Custom / ERP Module | Vendor Profile, Bid Submission, Delivery Status | Vendor-facing interface |
| Finance / AP System | ERP Module / Standalone | Invoice, Payment Term, 3-Way Match | Payment processing |

## Key Data Entities

### Vendor Master

```
vendor_id (PK)
vendor_name
category
contact_info
bank_account
certifications[]
status (active / blacklisted / pending)
risk_score
created_at
updated_at
```

### RFx Document

```
rfx_id (PK)
rfx_type (RFI / RFQ / RFP)
category
title
description
publish_date
submission_deadline
evaluation_criteria[]
status
created_by
```

### Bid / Proposal

```
bid_id (PK)
rfx_id (FK)
vendor_id (FK)
submitted_at
price
lead_time_days
technical_spec
attachments[]
score
rank
```

### Purchase Order

```
po_id (PK)
vendor_id (FK)
contract_id (FK)
line_items[]
total_amount
currency
delivery_date
status
approved_by
```

## Data Quality

Data quality is the foundation — the system will only work as well as the quality of the Vendor Master and historical data. Data cleansing should be planned before any system goes live.
