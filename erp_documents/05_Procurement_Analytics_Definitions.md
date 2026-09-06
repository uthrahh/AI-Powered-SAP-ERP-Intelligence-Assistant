# Procurement Analytics Definitions

**Company:** Apex Consumer Products (fictional company, synthetic PoC data)
**Document Type:** Synthetic Proof-of-Concept Enterprise Documentation
**Version:** 1.0
**Effective Date:** January 1, 2026
**Owner:** Procurement Analytics / FP&A

> **Disclaimer:** Synthetic PoC documentation. Metric definitions are illustrative and designed for RAG + Genie testing, not real financial reporting standards.

This document defines the business metrics and analytical concepts that the AI-Powered SAP ERP Intelligence Assistant must understand in order to answer analytics questions accurately and to reconcile them with knowledge-layer context (policy, process, glossary).

---

### Purchase Order Value
- **Business Definition:** The total monetary value of a single Purchase Order.
- **Calculation Logic:** Sum across all line items of (Quantity Ordered × Unit Price), i.e., SUM(MENGE × NETPR) across all EKPO rows for a given EBELN, excluding lines flagged for deletion (LOEKZ).
- **Relevant SAP Concepts:** EKKO (header), EKPO (items), MENGE, NETPR, LOEKZ
- **Important Filters:** Exclude deleted/cancelled lines; use order currency (WAERS) or convert to USD for cross-order comparison.
- **Common Synonyms:** "order total," "PO amount," "order size"
- **Assumptions:** Excludes tax and freight unless otherwise noted.

### Purchase Spend
- **Business Definition:** The total value of purchasing activity across a defined scope (all vendors, a time period, a category, etc.).
- **Calculation Logic:** SUM of Purchase Order Value across all in-scope, non-deleted POs within the filter criteria.
- **Relevant SAP Concepts:** EKKO, EKPO, BEDAT (for time filtering), BUKRS/EKORG (for org filtering)
- **Important Filters:** Time period (based on BEDAT), business unit/legal entity, category/purchasing group.
- **Common Synonyms:** "total spend," "procurement spend," "how much we bought"
- **Assumptions:** Reflects committed order value, not necessarily actual cash paid (see Invoice-based reporting for realized spend).

### Vendor Spend
- **Business Definition:** Total Purchase Spend attributable to a single vendor.
- **Calculation Logic:** SUM of Purchase Order Value for all non-deleted POs where LIFNR = the vendor in question.
- **Relevant SAP Concepts:** EKKO, EKPO, LFA1, LIFNR
- **Important Filters:** Time period; whether to include Pending (not-yet-approved) POs or only Approved ones.
- **Common Synonyms:** "how much we spend with [vendor]," "vendor total"
- **Assumptions:** Unless specified, includes all non-cancelled POs regardless of approval status; clarify with user if ambiguous.

### Average PO Value
- **Business Definition:** The mean value of Purchase Orders within a scope.
- **Calculation Logic:** Purchase Spend ÷ PO Count for the same filter scope.
- **Relevant SAP Concepts:** EKKO, EKPO
- **Important Filters:** Same scope filters as Purchase Spend and PO Count must match.
- **Common Synonyms:** "average order size," "typical PO amount"
- **Assumptions:** Simple arithmetic mean; not weighted or median unless requested.

### PO Count
- **Business Definition:** The number of distinct Purchase Orders within a scope.
- **Calculation Logic:** COUNT of distinct EBELN values meeting the filter criteria (typically excluding fully deleted/cancelled POs unless explicitly requested).
- **Relevant SAP Concepts:** EKKO
- **Important Filters:** Time period, vendor, status, business unit.
- **Common Synonyms:** "how many orders," "number of POs"
- **Assumptions:** Counts at header level, not line-item level.

### Open PO
- **Business Definition:** A Purchase Order (or line item) that has been approved and issued to the vendor but has not yet been fully received and/or fully invoiced.
- **Calculation Logic:** PO status = Approved/Released AND (Quantity Received < Quantity Ordered OR not fully invoiced), and not flagged for deletion.
- **Relevant SAP Concepts:** EKKO, EKPO, LOEKZ, goods receipt status
- **Important Filters:** Exclude Closed and Cancelled POs.
- **Common Synonyms:** "outstanding PO," "still-open order," "not yet delivered"
- **Assumptions:** "Open" refers to fulfillment status, distinct from "Pending," which refers to approval status.

### Pending PO
- **Business Definition:** A Purchase Order that has not yet completed its required approval chain (per the Procurement Policy value-tier thresholds).
- **Calculation Logic:** PO status = Pending Approval, i.e., at least one required approver for its value tier has not yet approved.
- **Relevant SAP Concepts:** EKKO (header status), approval workflow data (not a raw EKKO/EKPO field — sourced from workflow/approval logs)
- **Important Filters:** Value tier (to know which approvers are required); vendor block status.
- **Common Synonyms:** "awaiting approval," "not yet approved," "stuck in approval"
- **Assumptions:** A PO can be both "Pending" (not approved) — it cannot simultaneously be "Open" (which requires prior approval/release).

### Approved PO
- **Business Definition:** A Purchase Order that has received all required approvals for its value tier and been released to the vendor.
- **Calculation Logic:** PO status = Approved/Released.
- **Relevant SAP Concepts:** EKKO, approval workflow data
- **Important Filters:** Date approval completed, approver chain.
- **Common Synonyms:** "released PO," "cleared for vendor"

### Rejected PO
- **Business Definition:** A Purchase Order that an approver declined, sending it back to the requester/buyer rather than approving it.
- **Calculation Logic:** PO status = Rejected (workflow outcome), typically requiring resubmission as a revised PO.
- **Relevant SAP Concepts:** EKKO, approval workflow data
- **Important Filters:** Reason code for rejection, rejecting approver/role.
- **Common Synonyms:** "declined PO," "sent back," "denied order"

### PO Cycle Time
- **Business Definition:** The elapsed time from Purchase Order creation to full approval (or, in a broader definition, to full goods receipt/closure).
- **Calculation Logic:** (Date of final approval − BEDAT), measured in business days. A broader "full cycle time" variant measures (Closure Date − BEDAT).
- **Relevant SAP Concepts:** EKKO (BEDAT), approval workflow timestamps, goods receipt date
- **Important Filters:** Value tier (higher tiers naturally take longer due to more approvers); vendor.
- **Common Synonyms:** "how long approval takes," "order turnaround time," "time to approve"
- **Assumptions:** Unless specified, "PO Cycle Time" refers to approval cycle time, not full receipt-to-close cycle time — clarify with user if ambiguous.

### Vendor Performance
- **Business Definition:** A composite measure of how reliably and compliantly a vendor fulfills its Purchase Orders.
- **Calculation Logic:** Combination of On-Time Delivery Rate (Receipts on/before PO delivery date ÷ total receipts), Quality Defect Rate (rejected/defective receipts ÷ total receipts), and Invoice Accuracy Rate (invoices matching PO within tolerance ÷ total invoices).
- **Relevant SAP Concepts:** EKKO, EKPO, goods receipt data, invoice data, LFA1
- **Important Filters:** Time window (e.g., trailing 12 months); vendor classification.
- **Common Synonyms:** "how good is this vendor," "supplier scorecard," "vendor reliability"
- **Assumptions:** Requires goods-receipt and invoice data in addition to PO data; if only PO data is available, performance can only be partially estimated.

### High-value PO
- **Business Definition:** As defined in the Procurement Policy, any PO with total net value ≥ $25,000 (Tier 3 or Tier 4).
- **Calculation Logic:** Purchase Order Value ≥ $25,000 (converted to USD if needed).
- **Relevant SAP Concepts:** EKKO, EKPO
- **Important Filters:** Currency conversion basis; approval status.
- **Common Synonyms:** "big order," "large PO," "major purchase"
- **Assumptions:** Threshold is fixed per current policy version (1.0); must be re-checked if the Procurement Policy is updated.

### Monthly Spend
- **Business Definition:** Purchase Spend aggregated by calendar month.
- **Calculation Logic:** SUM(Purchase Order Value) grouped by MONTH(BEDAT).
- **Relevant SAP Concepts:** EKKO, EKPO, BEDAT
- **Important Filters:** Fiscal vs. calendar month (Apex uses calendar month for this metric); business unit.
- **Common Synonyms:** "spend by month," "monthly procurement trend"

### Category Spend
- **Business Definition:** Purchase Spend aggregated by product/material category (as defined in Material Master data) or by Purchasing Group as a proxy category.
- **Calculation Logic:** SUM(Purchase Order Value) grouped by material category (MARA-derived) or EKGRP.
- **Relevant SAP Concepts:** MARA, EKPO, EKGRP
- **Important Filters:** Category taxonomy version; time period.
- **Common Synonyms:** "spend by category," "spend by product line," "category-level spend"
- **Assumptions:** Category grouping in this synthetic PoC is simplified to a small set of illustrative categories (e.g., Packaging, Raw Materials, IT & Office, Facilities, Marketing Services).

*(End of Document 5 — Procurement Analytics Definitions)*
