# AI-Powered SAP ERP Intelligence Assistant — PoC Support Package

**Domain:** SAP Procurement | **Company:** Apex Consumer Products (fictional)
**Type:** Synthetic Proof-of-Concept Documentation

This document accompanies the six enterprise documents and provides: (1) a recommended folder structure, (2) a consolidated list of 32 evaluation questions with routing labels, and (3) an explanation of how each document contributes to the PoC.

---

## 1. Recommended Folder Structure

```
sap-procurement-intelligence-poc/
│
├── knowledge_base/                          # RAG source documents (Vector Search index source)
│   ├── 01_procurement_policy.md
│   ├── 02_purchase_order_process_sop.md
│   ├── 03_vendor_management_policy.md
│   ├── 04_sap_procurement_business_glossary.md
│   ├── 05_procurement_analytics_definitions.md
│   └── 06_procurement_faq_and_business_scenarios.md
│
├── structured_data/                         # Synthetic Delta tables (Unity Catalog managed)
│   ├── ekko_purchase_order_header.csv
│   ├── ekpo_purchase_order_item.csv
│   ├── lfa1_vendor_master.csv
│   └── mara_material_master.csv
│
├── unity_catalog/
│   ├── catalog_ddl/                         # CREATE CATALOG / SCHEMA / TABLE scripts
│   └── grants/                              # Access control definitions
│
├── vector_search/
│   ├── embedding_config.yaml                # Chunking + embedding model config for knowledge_base/
│   └── index_definition.json
│
├── genie/
│   └── genie_space_config.yaml              # Genie room config pointing at structured_data tables
│
├── orchestration/
│   ├── agent_router.py                      # Routes query -> RAG / Genie / Genie+RAG
│   ├── rag_agent.py
│   ├── genie_agent.py
│   └── synthesis_agent.py                   # Combines RAG + Genie outputs, applies glossary abstraction
│
├── apps/
│   └── databricks_app/                      # Front-end chat UI (Databricks Apps)
│
└── evaluation/
    ├── eval_questions.csv                   # The 32 questions below, machine-readable
    └── eval_results/                        # Test run outputs
```

---

## 2. Evaluation Question Set (32 Questions) with Routing Map

| # | Question | Route | Primary Source(s) |
|---|---|---|---|
| 1 | What is the PO approval process? | RAG | Doc 1, Doc 2 |
| 2 | When is Finance approval required on a purchase order? | RAG | Doc 1 |
| 3 | How do I onboard a new vendor? | RAG | Doc 3 |
| 4 | What documentation is required for a high-value purchase? | RAG | Doc 1 |
| 5 | What happens if a vendor is suspended? | RAG | Doc 3 |
| 6 | Can I split a large purchase into smaller orders to avoid approval? | RAG | Doc 1 |
| 7 | What is considered a high-value purchase order? | RAG | Doc 1, Doc 5 |
| 8 | What is the difference between "Open" and "Pending" for a PO? | RAG | Doc 5 |
| 9 | What is the escalation process if a PO issue isn't resolved? | RAG | Doc 2 |
| 10 | What are the vendor classifications and what do they mean? | RAG | Doc 3 |
| 11 | Which vendors have the highest spend this year? | Genie | EKKO, EKPO, LFA1 |
| 12 | How many purchase orders were created this month? | Genie | EKKO |
| 13 | What is our average PO value for Q1? | Genie | EKKO, EKPO |
| 14 | How many POs are currently open? | Genie | EKKO, EKPO |
| 15 | What is our total spend with [Vendor Name] this year? | Genie | EKKO, EKPO, LFA1 |
| 16 | Which product category had the highest spend last quarter? | Genie | EKPO, MARA |
| 17 | How many POs are still pending approval? | Genie | EKKO, workflow status |
| 18 | What is the total value of all POs created in March 2026? | Genie | EKKO, EKPO |
| 19 | List the top 5 largest purchase orders this year. | Genie | EKKO, EKPO |
| 20 | What currency are most of our vendor orders placed in? | Genie | EKKO |
| 21 | Why is PO 4500001234 pending? | Genie + RAG | EKKO/status + Doc 1 |
| 22 | Does this PO require Finance approval? | Genie + RAG | EKKO/EKPO value + Doc 1 |
| 23 | Is this purchase compliant with procurement policy? | Genie + RAG | EKKO/EKPO/LFA1 + Doc 1 |
| 24 | What should happen next for this PO? | Genie + RAG | EKKO status + Doc 2 |
| 25 | Which high-value POs are currently pending approval? | Genie + RAG | EKKO/EKPO + Doc 1 |
| 26 | Is this vendor eligible to receive a new PO right now? | Genie + RAG | LFA1 classification + Doc 3 |
| 27 | Why did this PO take longer than usual to get approved? | Genie + RAG | EKKO timestamps + Doc 1/2 |
| 28 | Are any high-value pending POs at risk of a compliance issue? | Genie + RAG | EKKO/EKPO/LFA1 + Doc 1 |
| 29 | Which vendor should this PO have gone to, and does the current vendor match? | Genie + RAG | LFA1 + Doc 3 |
| 30 | This PO exceeds its original approved value — what needs to happen? | Genie + RAG | EKKO/EKPO variance + Doc 1 |
| 31 | Can this emergency purchase be processed without full approval right now? | Genie + RAG | EKKO value + Doc 1 |
| 32 | How many open high-value POs lack an active MSA vendor? | Genie + RAG | EKKO/EKPO/LFA1 + Doc 1/2 |

**Routing summary:** 10 RAG-only, 10 Genie-only, 12 Genie+RAG — a deliberately balanced test set to validate the orchestration layer's routing logic across all three paths.

---

## 3. How Each Document Contributes to the PoC

- **Document 1 — Procurement Policy:** The rulebook. Supplies approval thresholds, high-value definitions, compliance rules, and exception handling that the assistant needs to *judge* structured data (e.g., "is this PO's approval status correct given its value?").

- **Document 2 — Purchase Order Process SOP:** The process map. Supplies lifecycle stages, role responsibilities, and escalation paths, enabling the assistant to answer "what stage is this PO at" and "what happens next" questions with procedural accuracy.

- **Document 3 — Vendor Management Policy:** The vendor rulebook. Supplies onboarding, classification, and suspension logic, enabling the assistant to interpret vendor status fields from structured data (LFA1-derived) in business terms and judge PO eligibility.

- **Document 4 — SAP Procurement Business Glossary:** The translation layer. This is the single most important document for the stated objective of "eliminating SAP complexity" — it is what lets the assistant convert EKKO/EKPO/LFA1/MARA/field-level technical output from Genie into plain business language, and vice versa (parsing a business question back into the right technical concepts to query).

- **Document 5 — Procurement Analytics Definitions:** The metrics contract. Ensures Genie-generated aggregations (spend, PO count, cycle time, etc.) are calculated and explained consistently with a documented business definition, rather than the LLM improvising its own metric logic per query.

- **Document 6 — Procurement FAQ and Business Scenarios:** The test harness and worked-example layer. Demonstrates, in worked examples, exactly how RAG-only, Genie-only, and combined answers should be structured — serving simultaneously as RAG retrieval content (similar questions can be matched semantically) and as the source for this evaluation set.

Together, these six documents give the LLM everything required to sit *between* Genie's structured output and the business user: enough policy/process/vendor context to interpret and reason (Documents 1–3), a precise vocabulary bridge (Document 4), a consistent metrics contract (Document 5), and calibration examples for how to phrase and route answers (Document 6).

*(End of Support Package)*
