# SAP Procurement Business Glossary

**Company:** Apex Consumer Products (fictional company, synthetic PoC data)
**Document Type:** Synthetic Proof-of-Concept Enterprise Documentation
**Version:** 1.0
**Effective Date:** January 1, 2026
**Owner:** Procurement Data Governance

> **Disclaimer:** This glossary uses realistic SAP-style terminology for a synthetic Proof-of-Concept. It is not official SAP standard documentation and does not represent real SAP configuration or naming exactly as SAP would define it in production systems.

## Purpose

This glossary maps SAP technical terminology (table names and field names) to business-friendly language. It is the core translation layer that allows the AI-Powered SAP ERP Intelligence Assistant to answer business questions without exposing SAP technical jargon to end users, and to correctly interpret business language back into the underlying structured data.

---

## Tables

### EKKO — Purchase Order Header
- **Business-Friendly Name:** Purchase Order (header-level information)
- **Plain-English Meaning:** Stores the "cover page" of a Purchase Order — the vendor, dates, currency, and overall order-level details that apply to all items on that order.
- **Business Usage:** Referenced whenever a user asks about a PO as a whole (its vendor, status, total value, or approval).
- **Related Concepts:** Purchase Order Item (EKPO), Vendor Master (LFA1)
- **How Business Users Refer to It:** "the PO," "the order," "the purchase order record" — they never say "EKKO."

### EKPO — Purchase Order Item
- **Business-Friendly Name:** Purchase Order Line Item
- **Plain-English Meaning:** Stores each individual line of a PO — the specific material or service, quantity, price, and delivery details for that line.
- **Business Usage:** Referenced when a user asks about specific products/quantities/prices within an order, or about partial receipts.
- **Related Concepts:** Purchase Order Header (EKKO), Material Master (MARA)
- **How Business Users Refer to It:** "the line item," "that item on the order," "the product on the PO"

### LFA1 — Vendor Master (General Data)
- **Business-Friendly Name:** Vendor / Supplier Record
- **Plain-English Meaning:** Stores general information about a vendor/supplier — name, address, country, and basic identifying details, independent of any specific purchasing organization.
- **Business Usage:** Referenced when a user asks "who is this vendor," "what vendor supplied this," or vendor lookups.
- **Related Concepts:** Purchase Order Header (EKKO), Vendor Classification (business concept, not a raw SAP field)
- **How Business Users Refer to It:** "the vendor," "the supplier," "the vendor record"

### MARA — Material Master (General Data)
- **Business-Friendly Name:** Product / Material Record
- **Plain-English Meaning:** Stores general information about a material or product — description, base unit of measure, material type/category — independent of plant or sales-specific details.
- **Business Usage:** Referenced when a user asks about a product's description, category, or unit of measure.
- **Related Concepts:** Purchase Order Item (EKPO)
- **How Business Users Refer to It:** "the product," "the item," "the material," "the SKU"

---

## Fields

### EBELN — Purchase Order Number
- **Business-Friendly Name:** PO Number
- **Plain-English Meaning:** The unique identifier assigned to a Purchase Order.
- **Business Usage:** Used to look up or reference a specific order.
- **Related Concepts:** EKKO (header), EKPO (items reference the same EBELN)
- **How Business Users Refer to It:** "PO number," "order number," e.g., "PO 4500001234"

### EBELP — Purchase Order Item Number
- **Business-Friendly Name:** PO Line Number
- **Plain-English Meaning:** The sequential number identifying a specific line item within a Purchase Order (e.g., line 10, 20, 30).
- **Business Usage:** Used when a PO has multiple products/lines and a specific one needs to be referenced.
- **Related Concepts:** EBELN (the parent order)
- **How Business Users Refer to It:** "line 1," "the first item," "item number"

### LIFNR — Vendor Number
- **Business-Friendly Name:** Vendor ID
- **Plain-English Meaning:** The unique identifier assigned to a vendor/supplier in the system.
- **Business Usage:** Links a PO to its vendor; used to look up vendor details.
- **Related Concepts:** LFA1 (vendor master), EKKO (header references LIFNR)
- **How Business Users Refer to It:** "vendor ID," "supplier code," or simply the vendor's name

### MATNR — Material Number
- **Business-Friendly Name:** Product ID / SKU
- **Plain-English Meaning:** The unique identifier assigned to a specific product or material.
- **Business Usage:** Links a PO line item to its product master data.
- **Related Concepts:** MARA (material master), EKPO (item references MATNR)
- **How Business Users Refer to It:** "SKU," "product code," "item number" (not to be confused with EBELP)

### BEDAT — Purchase Order Date
- **Business-Friendly Name:** PO Creation Date / Order Date
- **Plain-English Meaning:** The date the Purchase Order was created/issued.
- **Business Usage:** Used for time-based analysis (e.g., "POs created this month").
- **Related Concepts:** EKKO
- **How Business Users Refer to It:** "order date," "when the PO was placed," "PO date"

### MENGE — Order Quantity
- **Business-Friendly Name:** Quantity Ordered
- **Plain-English Meaning:** The quantity of a material ordered on a specific PO line.
- **Business Usage:** Used in spend calculations (Quantity × Price) and receipt-matching.
- **Related Concepts:** EKPO, NETPR
- **How Business Users Refer to It:** "how many units," "quantity ordered"

### NETPR — Net Price
- **Business-Friendly Name:** Unit Price
- **Plain-English Meaning:** The negotiated price per unit for a material on a PO line, excluding tax.
- **Business Usage:** Core input to calculating PO Value and Spend metrics.
- **Related Concepts:** EKPO, MENGE, WAERS
- **How Business Users Refer to It:** "the price," "unit cost," "price per unit"

### WAERS — Currency Key
- **Business-Friendly Name:** Order Currency
- **Plain-English Meaning:** The currency in which the Purchase Order is denominated (e.g., USD, EUR).
- **Business Usage:** Required to correctly interpret and convert monetary values for cross-currency spend analysis.
- **Related Concepts:** EKKO, NETPR
- **How Business Users Refer to It:** "the currency," "what currency is this order in"

### LOEKZ — Deletion Indicator
- **Business-Friendly Name:** Cancelled / Deleted Flag
- **Plain-English Meaning:** A flag indicating that a PO or PO line has been marked for deletion/cancellation and should be excluded from active/open reporting.
- **Business Usage:** Used to filter out cancelled orders/lines from "open PO" or spend analysis.
- **Related Concepts:** EKKO, EKPO
- **How Business Users Refer to It:** "cancelled," "deleted," "voided" — business users would never say "deletion indicator" or "LOEKZ"

### BUKRS — Company Code
- **Business-Friendly Name:** Legal Entity / Business Unit
- **Plain-English Meaning:** The identifier for the legal entity/company within Apex's corporate structure that the PO belongs to, for financial reporting purposes.
- **Business Usage:** Used to segment spend analysis by legal entity or business unit.
- **Related Concepts:** EKKO, EKORG
- **How Business Users Refer to It:** "business unit," "legal entity," "which company"

### EKORG — Purchasing Organization
- **Business-Friendly Name:** Purchasing Division
- **Plain-English Meaning:** The organizational unit responsible for procurement activities and vendor negotiations for a defined scope (e.g., a region or business line).
- **Business Usage:** Used to segment reporting by which procurement team/division owns the vendor relationship.
- **Related Concepts:** EKKO, BUKRS
- **How Business Users Refer to It:** "procurement team," "sourcing division," "purchasing group's parent org"

### EKGRP — Purchasing Group
- **Business-Friendly Name:** Buyer Team / Category Team
- **Plain-English Meaning:** The specific team or individual buyer group responsible for day-to-day handling of a PO within a Purchasing Organization.
- **Business Usage:** Used to route questions like "who is the buyer responsible for this PO" or to segment reporting by category team.
- **Related Concepts:** EKKO, EKORG
- **How Business Users Refer to It:** "buyer group," "category team," "the buyer's team"

---

## Translation Principle for the Assistant

When responding to business users, the assistant should:
1. Never surface raw table names (EKKO, EKPO, LFA1, MARA) or field codes (EBELN, LIFNR, MATNR, etc.) in its answers.
2. Use the Business-Friendly Name or plain-language equivalent instead (e.g., "PO number" instead of "EBELN", "vendor" instead of "LIFNR").
3. Internally, the assistant (via Genie/structured queries) may still reference these technical names to retrieve data — the abstraction happens only in the final answer presented to the user.

*(End of Document 4 — SAP Procurement Business Glossary)*
