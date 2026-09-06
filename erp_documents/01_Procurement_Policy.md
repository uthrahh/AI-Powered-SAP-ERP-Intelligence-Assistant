# Procurement Policy

**Company:** Apex Consumer Products (fictional company, synthetic PoC data)
**Document Type:** Synthetic Proof-of-Concept Enterprise Documentation
**Domain:** Procurement
**Version:** 1.0
**Effective Date:** January 1, 2026
**Owner:** Global Procurement Office
**Status:** Approved

> **Disclaimer:** This document is entirely synthetic and was generated for a Proof-of-Concept ("AI-Powered SAP ERP Intelligence Assistant"). It does not represent real SAP standard configuration, real company policy, or confidential information of any real organization. Any resemblance to actual companies, vendors, or policies is coincidental.

---

## 1. Purpose and Scope

This Procurement Policy defines the rules, approval thresholds, and controls that govern how Apex Consumer Products ("Apex") purchases goods and services from external vendors. It applies to all employees, cost center owners, and procurement staff who create, approve, or manage Purchase Orders (POs) across all business units and plants.

The policy covers direct materials (raw materials, packaging, components used in production) and indirect materials/services (office supplies, IT equipment, contracted services, marketing, facilities).

This policy does not cover intercompany transfers, capital asset purchases above $500,000 (governed by the separate Capital Expenditure Policy), or employee expense reimbursements.

## 2. Purchase Order Approval Thresholds

All Purchase Orders at Apex are approved based on the **total net order value** (quantity × net price, before tax, in the PO's transaction currency, converted to USD for threshold evaluation).

| Threshold Tier | PO Value (USD) | Required Approver(s) |
|---|---|---|
| Tier 1 — Low Value | Up to $4,999.99 | Requester's direct manager (Cost Center Owner) |
| Tier 2 — Standard | $5,000.00 – $24,999.99 | Procurement Manager |
| Tier 3 — High Value | $25,000.00 – $99,999.99 | Director of Procurement **and** Finance Controller |
| Tier 4 — Strategic/Major | $100,000.00 and above | VP of Procurement, CFO, **and** Executive Committee sign-off |

**High-value purchase**, for the purposes of this policy and all related documents, is defined as any Purchase Order with a total net value of **$25,000 or greater** (Tier 3 or Tier 4).

## 3. Approval Hierarchy

Approval routing is sequential and cumulative — a PO is not considered "Approved" until every required approver for its tier has approved it.

1. **Cost Center Owner** — validates business need and budget availability.
2. **Procurement Manager** — validates sourcing strategy, vendor selection, and pricing (required from Tier 2 upward).
3. **Director of Procurement** — validates strategic vendor fit and contract terms (required from Tier 3 upward).
4. **Finance Controller** — validates budget impact and financial risk (required from Tier 3 upward).
5. **VP of Procurement** — validates alignment with category strategy (Tier 4 only).
6. **CFO** — validates enterprise financial exposure (Tier 4 only).
7. **Executive Committee** — final sign-off for strategic commitments (Tier 4 only).

A PO awaiting any one of these approvals is considered to be in **Pending Approval** status.

## 4. Rules for High-Value Purchases (Tier 3 and Tier 4)

- A minimum of **three competitive quotes** must be documented before PO creation, unless the vendor is a Sole Source Vendor (see Vendor Management Policy).
- Contracts above $100,000 require Legal review before PO issuance.
- Tier 4 purchases require a documented business case attached to the requisition.
- High-value POs to a vendor without an active Master Service Agreement (MSA) are automatically flagged for Director of Procurement review, regardless of value.
- Split-ordering (dividing one purchase into multiple smaller POs to avoid a higher approval tier) is strictly prohibited and considered a compliance violation.

## 5. Vendor Requirements

- All vendors must have an active, non-blocked Vendor Master record before a PO can be issued against them.
- Vendors must be classified as **Approved**, **Preferred**, or **Conditional** (see Vendor Management Policy) to receive new POs. **Suspended** or **Under Review** vendors cannot receive new POs.
- Vendors must have valid tax registration, banking details, and a signed Code of Conduct acknowledgment on file.
- Preferred Vendors are prioritized for sourcing events but do not bypass approval thresholds.

## 6. Purchase Order Compliance Rules

A PO is considered **compliant** when it satisfies all of the following:
- The PO has received all required approvals for its value tier.
- The vendor is Approved, Preferred, or Conditional (not Suspended).
- The PO references a valid Material Master record and Purchasing Organization.
- The PO currency and payment terms match the vendor's master data or an approved exception.
- For Tier 3/4 POs, competitive quotes or sole-source justification are documented.

A PO is considered **non-compliant** if any of the above conditions are not met, even if it has technically been released in the system. Non-compliant POs must be flagged for review by the Procurement Manager.

## 7. Exceptions

- **Emergency Purchases:** In documented emergencies (e.g., production line stoppage), a PO may be issued with verbal approval from the Cost Center Owner, but formal approval documentation must be completed within 3 business days retroactively. Emergency POs are still subject to the same value-tier approval requirements.
- **Blanket/Framework POs:** Recurring purchases under a pre-approved framework agreement may use a Blanket PO approved once at contract signing; individual releases against it do not require re-approval as long as they remain within the framework's total value and duration.
- **Currency Exceptions:** Non-USD POs are evaluated against thresholds using the exchange rate in effect on the PO creation date.

## 8. Financial Controls

- Procurement and Accounts Payable maintain segregation of duties: the person who creates a PO cannot also approve it, and the person who approves a PO cannot also record the goods receipt.
- All approvals must be captured with a timestamp and approver identity for audit purposes.
- Finance performs a quarterly audit of all Tier 3 and Tier 4 POs for compliance with this policy.
- Any PO exceeding its approved value by more than 10% at invoice time requires a new approval cycle before payment is released.

## 9. Roles and Responsibilities

| Role | Responsibility |
|---|---|
| Requester | Initiates purchase requisition with business justification |
| Cost Center Owner | Confirms budget availability; first-level approval |
| Procurement Manager | Vendor selection, sourcing, Tier 2 approval |
| Director of Procurement | Strategic review, Tier 3 approval |
| Finance Controller | Budget/financial risk review, Tier 3 approval |
| VP of Procurement / CFO / Executive Committee | Tier 4 strategic sign-off |
| Accounts Payable | Invoice matching and payment, independent of approval chain |

## 10. Effective Date and Version History

| Version | Date | Change |
|---|---|---|
| 1.0 | 2026-01-01 | Initial synthetic PoC policy issued |

*(End of Document 1 — Procurement Policy)*
