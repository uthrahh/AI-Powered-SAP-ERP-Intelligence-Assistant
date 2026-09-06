# Vendor Management Policy

**Company:** Apex Consumer Products (fictional company, synthetic PoC data)
**Document Type:** Synthetic Proof-of-Concept Enterprise Documentation
**Version:** 1.0
**Effective Date:** January 1, 2026
**Owner:** Global Procurement Office / Finance

> **Disclaimer:** Synthetic PoC documentation. Not real SAP configuration or real company policy.

---

## 1. Purpose

This policy governs how vendors are onboarded, classified, approved, maintained, and — where necessary — suspended or deactivated at Apex Consumer Products. It ensures that only compliant, financially sound, and properly documented vendors can receive Purchase Orders, in alignment with the Procurement Policy and Purchase Order Process SOP.

## 2. Vendor Onboarding

1. **Request:** A Buyer or Cost Center Owner submits a New Vendor Request with business justification.
2. **Data Collection:** The prospective vendor submits company registration documents, tax ID, banking details, insurance certificates, and a signed Code of Conduct.
3. **Risk Screening:** Finance and Compliance perform a credit check and sanctions/watchlist screening.
4. **Master Data Creation:** Procurement creates the Vendor Master record (general data, company-code-specific data, and purchasing-organization-specific data).
5. **Activation:** Once screening passes, the vendor is set to **Active** status and assigned an initial classification.

Vendors cannot receive a Purchase Order until master data creation and activation are complete.

## 3. Vendor Classification

Every vendor is assigned one classification, which determines sourcing eligibility:

| Classification | Description |
|---|---|
| **Preferred** | Strategic vendors with a Master Service Agreement, strong performance history, and negotiated pricing. Prioritized for new sourcing events. |
| **Approved** | Vendors who have passed onboarding and screening and may receive standard POs. |
| **Conditional** | Vendors approved for a limited scope (e.g., one project, one plant, or a capped spend amount) pending full qualification. |
| **Under Review** | Vendors flagged for a compliance, quality, or financial concern; existing POs may continue but no new POs are issued until review completes. |
| **Suspended** | Vendors blocked from receiving any new Purchase Orders due to a compliance failure, sanctions hit, quality failure, or contract breach. |

Only **Preferred**, **Approved**, and **Conditional** vendors may receive new Purchase Orders, consistent with the Procurement Policy.

## 4. Vendor Approval

- Initial approval requires sign-off from Procurement (sourcing fit) and Finance (financial/credit risk).
- Vendors supplying regulated categories (e.g., food-contact packaging, safety equipment) additionally require Quality/Compliance sign-off.
- Reclassification from Conditional to Approved requires a documented performance review after the initial qualifying period (typically 6 months or the first 3 completed POs, whichever is later).
- Reclassification to Preferred requires an active Master Service Agreement and at least 12 months of on-time, compliant performance.

## 5. Vendor Master Data Requirements

Vendor Master records must include and keep current:
- Legal name, address, and country of registration
- Tax identification number
- Banking details for payment processing
- Primary and secondary contact information
- Currency and standard payment terms
- Purchasing organization(s) the vendor is enabled for
- Classification status and effective date
- Insurance and compliance certificate expiration dates

Vendor Master data must be reviewed and re-confirmed at least annually; expired compliance documents automatically move a vendor to **Under Review**.

## 6. Vendor Compliance

Vendors are expected to comply with:
- Apex's Supplier Code of Conduct (labor, environmental, and ethical standards)
- Agreed delivery lead times and quality specifications
- Invoicing accuracy consistent with PO terms (price, quantity, currency)
- Maintaining valid insurance and, where applicable, regulatory certifications

Procurement conducts periodic vendor performance reviews (see Procurement Analytics Definitions for "Vendor Performance" metric) covering on-time delivery, quality defect rate, and invoice accuracy.

## 7. Vendor Suspension / Deactivation

A vendor may be moved to **Suspended** for:
- Failing a sanctions/watchlist re-screen
- Repeated quality failures (3 or more defect incidents within 12 months)
- Confirmed Code of Conduct violation
- Financial instability (e.g., credit rating downgrade below acceptable threshold)
- Legal or contractual breach

**Effects of suspension:**
- No new Purchase Orders may be created against a Suspended vendor.
- Existing open POs are reviewed by the Procurement Manager; they may be allowed to complete, be amended, or be cancelled depending on severity.
- Suspension requires sign-off from Director of Procurement and Finance Controller.

Vendors may be **deactivated** entirely (removed from active sourcing) after 24 months of no transaction activity or upon mutual contract termination. Deactivated vendors' historical PO data is retained for audit purposes.

## 8. Responsibilities of Procurement and Finance

| Role | Responsibility |
|---|---|
| Procurement Manager | Vendor sourcing, classification recommendations, performance reviews |
| Director of Procurement | Approval of Preferred classification and suspension decisions |
| Finance Controller | Credit risk assessment, banking data validation, suspension co-approval |
| Compliance/Quality | Regulatory and Code-of-Conduct screening, defect tracking |
| Accounts Payable | Reporting invoice-level compliance issues back to Procurement |

*(End of Document 3 — Vendor Management Policy)*
