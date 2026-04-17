# Step 1: Need Identification

## Overview

The P2P cycle begins when a department identifies a need for goods or services. The requester creates a **Purchase Requisition (PR)** specifying what is needed, how much, the budget, and when it is needed. The PR must go through an internal approval chain before procurement can begin sourcing.

## Actors

- **Requester** — the person who needs the goods/services (e.g., IT Engineer)
- **Department Head** — first-level approval
- **Department Manager** — second-level approval
- **Procurement Team** — receives approved PR and begins sourcing

## Process Steps

```
Identify Need → Create PR → Department Head Approval → Department Manager Approval → Procurement Receives PR
```

1. **Identify Need** — department determines a need for goods or services
2. **Create PR** — requester fills in the PR form with item details, specs, quantities, budget, and justification
3. **Approval Chain** — PR is routed through approvers (department head → department manager → procurement)
4. **Procurement Receives PR** — once approved, procurement begins the sourcing process

## Purchase Requisition (PR) Document

### Key Fields

| Field | Description |
|-------|------------|
| PR Number | Unique identifier (e.g., PR-2024-0892) |
| Requesting Department | Department that needs the goods/services |
| Requester | Person creating the PR with role |
| Request Date | Date the PR was created |
| Required Date | Date by which goods/services are needed |
| Procurement Type | Direct or Indirect (e.g., Indirect — IT Equipment) |
| Budget Allocation | Approved budget reference (e.g., CAPEX Budget Q1/2567) |

### Line Items Structure

| Field | Description |
|-------|------------|
| Item Number | Sequential number |
| Item Name | Name of product/service |
| Specification | Detailed description / spec |
| Quantity | Required quantity |
| Unit | Unit of measure |
| Estimated Price | Budget estimate per unit |

### Justification

The PR must include a business justification explaining why the purchase is necessary. Example: equipment over 4 years old causing reduced productivity for 5 developers, replacement needed for a new project starting in Q1-2.

### Approval Signatures

| Role | Responsibility |
|------|---------------|
| Requester | Creates and submits the PR |
| Department Head | Validates the business need |
| Department Manager | Approves within department budget |
| Procurement Team | Accepts and begins sourcing |

## Related Documents

- Output: Approved PR triggers [Step 2: Sourcing](02-sourcing.md)

## Related Mock Data

- [purchase-requisitions.json](../mock-data/purchase-requisitions.json)
