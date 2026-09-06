# Procurement FAQ and Business Scenarios

**Company:** Apex Consumer Products (fictional company, synthetic PoC data)
**Document Type:** Synthetic Proof-of-Concept Enterprise Documentation
**Version:** 1.0
**Effective Date:** January 1, 2026
**Owner:** Procurement Operations / AI Assistant Enablement Team

> **Disclaimer:** Synthetic PoC documentation. Scenarios and vendor/PO numbers are fictional examples for RAG/Genie testing.

This document provides realistic business questions across three categories, with guidance on what each requires to answer correctly. It is designed to test and calibrate the AI-Powered SAP ERP Intelligence Assistant's routing between Knowledge (RAG), Analytics (Genie), and combined intelligence.

---

## A. Knowledge Questions (RAG only)

These can be answered entirely from policy/process/glossary documents, with no need to query live transactional data.

1. **What is the PO approval process?**
   - Requires: Procurement Policy + PO Process SOP
   - Route: RAG
   - Answer should contain: The tiered approval thresholds and who approves at each tier, plus the sequence of lifecycle stages.

2. **When is Finance approval required on a purchase order?**
   - Requires: Procurement Policy (Section 2–3)
   - Route: RAG
   - Answer should contain: Finance Controller approval is required starting at Tier 3 ($25,000+), alongside Director of Procurement.

3. **How do I onboard a new vendor?**
   - Requires: Vendor Management Policy (Section 2)
   - Route: RAG
   - Answer should contain: The 5-step onboarding flow (request, data collection, risk screening, master data creation, activation).

4. **What documentation is required for a high-value purchase?**
   - Requires: Procurement Policy (Section 4)
   - Route: RAG
   - Answer should contain: Three competitive quotes (or sole-source justification), Legal review above $100,000, business case for Tier 4.

5. **What happens if a vendor is suspended?**
   - Requires: Vendor Management Policy (Section 7)
   - Route: RAG
   - Answer should contain: No new POs can be issued; existing POs are reviewed by the Procurement Manager.

6. **Can I split a large purchase into smaller orders to avoid approval?**
   - Requires: Procurement Policy (Section 4)
   - Route: RAG
   - Answer should contain: This is explicitly prohibited ("split-ordering") and is a compliance violation.

7. **What is considered a high-value purchase order?**
   - Requires: Procurement Policy / Analytics Definitions
   - Route: RAG
   - Answer should contain: $25,000 or greater (Tier 3 or Tier 4).

8. **What is the difference between "Open" and "Pending" for a PO?**
   - Requires: Analytics Definitions (Open PO, Pending PO)
   - Route: RAG
   - Answer should contain: Pending = not yet fully approved; Open = approved but not yet fully received/invoiced.

9. **What is the escalation process if a PO issue isn't resolved?**
   - Requires: PO Process SOP (Section 7)
   - Route: RAG
   - Answer should contain: The 4-level escalation path from Buyer up to Executive Committee for Tier 4.

10. **What are the vendor classifications and what do they mean?**
    - Requires: Vendor Management Policy (Section 3)
    - Route: RAG
    - Answer should contain: Preferred, Approved, Conditional, Under Review, Suspended, with eligibility for new POs.

---

## B. Analytics Questions (Genie only)

These require querying structured transactional data and do not require policy interpretation.

11. **Which vendors have the highest spend this year?**
    - Requires: Aggregation of PO Value by vendor (EKKO/EKPO/LFA1)
    - Route: Genie
    - Answer should contain: A ranked list of vendors by total spend, presented with business-friendly vendor names, not LIFNR codes.

12. **How many purchase orders were created this month?**
    - Requires: COUNT(EBELN) filtered by BEDAT
    - Route: Genie
    - Answer should contain: A count, with the month clearly stated.

13. **What is our average PO value for Q1?**
    - Requires: Purchase Spend ÷ PO Count for Q1
    - Route: Genie

14. **How many POs are currently open?**
    - Requires: COUNT of POs meeting the "Open PO" definition
    - Route: Genie

15. **What is our total spend with [Vendor Name] this year?**
    - Requires: SUM(PO Value) filtered by vendor and year
    - Route: Genie

16. **Which product category had the highest spend last quarter?**
    - Requires: Category Spend aggregation
    - Route: Genie

17. **How many POs are still pending approval?**
    - Requires: COUNT of POs with status = Pending Approval
    - Route: Genie

18. **What is the total value of all purchase orders created in March 2026?**
    - Requires: SUM(PO Value) filtered by BEDAT = March 2026
    - Route: Genie

19. **List the top 5 largest purchase orders this year.**
    - Requires: Rank POs by value, TOP 5
    - Route: Genie

20. **What currency are most of our vendor orders placed in?**
    - Requires: Aggregation/mode of WAERS across POs
    - Route: Genie

---

## C. Intelligence Questions Requiring BOTH Structured Data and Knowledge

These require pulling specific transactional facts (Genie) and interpreting them against policy/process context (RAG).

21. **Why is PO 4500001234 pending?**
    - Requires: (Genie) Current approval status and value tier of that specific PO; (RAG) which approvers are required at that tier and what conditions cause "Pending" status.
    - Route: Genie + RAG
    - Correct answer should contain: The specific missing approval (e.g., "awaiting Finance Controller sign-off because this order is $42,000, which falls in the $25,000–$99,999 tier requiring both Director of Procurement and Finance Controller approval").

22. **Does this PO require Finance approval?**
    - Requires: (Genie) The PO's value; (RAG) the threshold rule that Finance Controller approval starts at $25,000.
    - Route: Genie + RAG
    - Correct answer should contain: A yes/no determination plus the specific value and threshold reasoning.

23. **Is this purchase compliant with procurement policy?**
    - Requires: (Genie) PO's vendor classification, approval status, quote documentation flag; (RAG) the compliance rules in the Procurement Policy (Section 6).
    - Route: Genie + RAG
    - Correct answer should contain: A compliant/non-compliant determination with the specific rule(s) checked.

24. **What should happen next for this PO?**
    - Requires: (Genie) Current lifecycle stage/status; (RAG) the next step defined in the PO Process SOP.
    - Route: Genie + RAG
    - Correct answer should contain: The next action and who is responsible for it (e.g., "vendor confirmation is outstanding; Buyer should follow up since it has been 6 business days").

25. **Which high-value POs are currently pending approval?**
    - Requires: (Genie) Filter POs where value ≥ $25,000 AND status = Pending; (RAG) confirmation that $25,000 is the high-value threshold.
    - Route: Genie + RAG

26. **Is this vendor eligible to receive a new PO right now?**
    - Requires: (Genie) Vendor's current classification status; (RAG) which classifications allow new POs.
    - Route: Genie + RAG
    - Correct answer should contain: Eligible/not eligible, with the vendor's classification and the rule that Suspended/Under Review vendors cannot receive new POs.

27. **Why did this PO take longer than usual to get approved?**
    - Requires: (Genie) PO's cycle time and value tier vs. peer average; (RAG) explanation that higher tiers require more approvers, which naturally extends cycle time.
    - Route: Genie + RAG

28. **Are any of our high-value pending POs at risk of a compliance issue?**
    - Requires: (Genie) High-value pending POs with missing documentation flags or vendors not Approved/Preferred; (RAG) the compliance rules defining risk conditions.
    - Route: Genie + RAG

29. **Which vendor should this PO have gone to given our sourcing rules, and does the current vendor match?**
    - Requires: (Genie) Vendor currently on the PO and its classification/spend history; (RAG) sourcing preference rules for Preferred vendors.
    - Route: Genie + RAG

30. **This PO exceeds its original approved value — what needs to happen?**
    - Requires: (Genie) Original approved value vs. current/invoice value, percentage variance; (RAG) the rule that >10% overage requires a new approval cycle.
    - Route: Genie + RAG
    - Correct answer should contain: The variance percentage and whether it triggers the re-approval rule.

31. **Can this emergency purchase be processed without full approval right now?**
    - Requires: (Genie) PO value/tier; (RAG) the Emergency Purchase exception rules (verbal approval, 3-day retroactive documentation).
    - Route: Genie + RAG

32. **How many of our currently open high-value POs are with vendors that don't have an active Master Service Agreement?**
    - Requires: (Genie) Open + high-value POs joined to vendor MSA status; (RAG) the rule that such POs are auto-flagged for Director of Procurement review.
    - Route: Genie + RAG

---

## Guidance for the Assistant

- **RAG-only** questions should never require a live data query — answer from policy/process/glossary/analytics-definition context.
- **Genie-only** questions should never require policy interpretation — answer purely from structured data, but still translate technical field names into business language per the Glossary.
- **Genie + RAG** questions must combine a specific data lookup with a rule from the knowledge layer, and the final answer must explain the "why," not just present a number or status.

*(End of Document 6 — Procurement FAQ and Business Scenarios)*
