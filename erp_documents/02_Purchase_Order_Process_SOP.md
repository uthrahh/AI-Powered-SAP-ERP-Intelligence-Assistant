# Purchase Order Process — Standard Operating Procedure (SOP)

**Company:** Apex Consumer Products (fictional company, synthetic PoC data)
**Document Type:** Synthetic Proof-of-Concept Enterprise Documentation
**Version:** 1.0
**Effective Date:** January 1, 2026
**Owner:** Global Procurement Operations

> **Disclaimer:** Synthetic PoC documentation. Not real SAP configuration or real company process.

---

## 1. Purpose

This SOP describes the end-to-end lifecycle of a Purchase Order (PO) at Apex Consumer Products, from initial requisition through closure, and defines who performs each step, what triggers delays, and how exceptions are escalated. This document is aligned with the thresholds and roles defined in the Procurement Policy.

## 2. End-to-End Purchase Order Lifecycle

The PO lifecycle consists of six stages:

### Stage 1 — Requisition
- **Performed by:** Requester (any employee with a valid cost center)
- The requester submits a Purchase Requisition specifying material/service, quantity, needed-by date, cost center, and business justification.
- The requisition is routed to the Cost Center Owner for budget validation.

### Stage 2 — Purchase Order Creation
- **Performed by:** Buyer / Procurement Analyst
- Once the requisition is validated, a Buyer selects or confirms the vendor, negotiates pricing if needed, and creates the Purchase Order with header information (vendor, purchasing organization, purchasing group, currency, payment terms) and line items (material, quantity, price, delivery date, plant).
- A newly created PO enters status **Draft** until submitted for approval.

### Stage 3 — Approval
- **Performed by:** Approvers per the value-tier hierarchy defined in the Procurement Policy.
- The PO is routed automatically based on total net value:
  - Tier 1 (< $5,000): Cost Center Owner only.
  - Tier 2 ($5,000–$24,999): + Procurement Manager.
  - Tier 3 ($25,000–$99,999): + Director of Procurement and Finance Controller.
  - Tier 4 (≥ $100,000): + VP of Procurement, CFO, Executive Committee.
- A PO remains in **Pending Approval** status until every required approver has signed off.
- Once fully approved, the PO status changes to **Approved / Released** and is transmitted to the vendor.

### Stage 4 — Vendor Confirmation
- **Performed by:** Vendor, tracked by Buyer
- The vendor confirms receipt of the PO and acknowledges quantity, price, and delivery date, or proposes changes (a "vendor confirmation with deviation").
- If the vendor proposes deviations, the Buyer must re-negotiate or obtain re-approval if the deviation changes the PO's value tier.
- Unconfirmed POs after 5 business days are flagged for Buyer follow-up.

### Stage 5 — Goods/Service Receipt
- **Performed by:** Warehouse/Receiving staff (goods) or requester (services)
- Upon delivery, a Goods Receipt (GR) is posted against the PO line item, recording quantity received and date.
- Partial receipts are allowed; the PO line remains **Open** until the full ordered quantity is received or the line is manually closed.
- Discrepancies (short/over/damaged delivery) trigger a Goods Receipt exception, routed to the Buyer and Quality team.

### Stage 6 — Invoice Matching and Closure
- **Performed by:** Accounts Payable
- Accounts Payable performs a 3-way match (PO, Goods Receipt, Vendor Invoice). If all three match within tolerance (typically ±2% or ±$50, whichever is greater), the invoice is approved for payment.
- Once all line items are fully received, invoiced, and paid, the PO status changes to **Closed**.
- A PO can also be manually closed ("technically completed") if remaining open quantity will not be delivered.

## 3. Conditions That Cause a PO to Become Pending

A PO enters or remains in **Pending** status when any of the following are true:
- One or more required approvers (per its value tier) has not yet approved it.
- An approver has requested changes ("sent back for revision").
- The vendor is not yet Approved/Preferred/Conditional in the Vendor Master (blocked vendor).
- Budget validation at the Cost Center level has failed or budget has been exhausted.
- A vendor-proposed deviation pushed the PO into a higher value tier, requiring additional approval.
- Required documentation (competitive quotes, sole-source justification) is missing for Tier 3/4 POs.

## 4. Approval Routing Logic

Routing is value-tier driven and cumulative, as described in the Procurement Policy. Additional routing rules:
- If a vendor has no active Master Service Agreement, the PO is automatically routed to the Director of Procurement for an extra review step, regardless of tier.
- If the requester's cost center is over budget for the period, the PO is routed back to the Cost Center Owner before any procurement-level approval occurs.
- Emergency Purchases follow expedited routing: verbal Cost Center Owner approval unblocks PO issuance, with formal approval completed within 3 business days.

## 5. Required Information for PO Creation

- Purchasing Organization and Purchasing Group
- Vendor (must exist and be active in Vendor Master)
- Material or service description (linked to Material Master where applicable)
- Quantity and Unit of Measure
- Net Price and Currency
- Delivery/Plant location and required delivery date
- Payment terms
- Cost center / account assignment
- Requisition reference (if applicable)

## 6. Common Exceptions

| Exception | Description | Typical Resolution |
|---|---|---|
| Price mismatch at invoice | Invoice price differs from PO price beyond tolerance | AP routes to Buyer for investigation |
| Quantity mismatch | Goods received differ from PO quantity | Buyer contacts vendor; may issue PO amendment |
| Vendor blocked mid-cycle | Vendor suspended after PO issued but before receipt | Procurement Manager reviews; PO may be cancelled or vendor reinstated |
| Duplicate PO | Same requisition converted into two POs | Procurement Analyst cancels duplicate |
| Budget overrun | Actual cost exceeds approved budget | Requires new approval cycle |
| Deletion flag set | PO or line marked for deletion before completion | PO/line excluded from open-order reporting |

## 7. Escalation Procedure

1. **Level 1:** Buyer attempts resolution directly with vendor or requester (target: 2 business days).
2. **Level 2:** If unresolved, Procurement Manager is notified and intervenes (target: 3 additional business days).
3. **Level 3:** For Tier 3/4 POs or unresolved vendor compliance issues, Director of Procurement and Finance Controller are notified.
4. **Level 4:** Executive Committee is engaged only for Tier 4 POs with unresolved strategic or financial risk.

Escalations must be logged with a reason code and resolution outcome for audit purposes.

*(End of Document 2 — Purchase Order Process SOP)*
