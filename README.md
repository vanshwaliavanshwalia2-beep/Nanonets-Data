# Enterprise Automation & Intelligent Document Processing (IDP) Suite

A comprehensive suite of enterprise-grade automation tools combining **Intelligent Document Processing (IDP)**, **Machine Learning**, **Business Intelligence**, and **Asynchronous Workflows**. This repository contains production-ready pipelines for automated financial credit risk routing and AI-powered invoice extraction.

---

## 📂 Module 1: Automated Credit Risk Assessment

An end-to-end automated pipeline built with **n8n** that ingests financial application data from **Google Sheets**, evaluates applicants through multi-tiered conditional risk logic, updates tracking sheets in real time, and sends automated decision notifications via **Gmail**.

### 🚀 Core Architecture & Workflow
The automation engine is driven by an asynchronous node-based workflow in n8n. It processes batch applications sequentially, passing them through structured evaluation matrices (`IF` filters) to arrive at three primary states: *Auto-Approve*, *Manual Review*, or *Auto-Reject*.

#### Workflow Visual Map
<img src="./workflow.jpeg" alt="n8n Automated Decisioning Workflow" width="100%"/>

#### Workflow Breakdown
1. **Trigger**: Manually executed or webhook-driven initiation (`When clicking 'Execute workflow'`).
2. **Data Ingestion**: Pulls raw applicant profiles from a secure Google Sheet ledger.
3. **Conditional Logic Filters (`If`, `If1`, `If2`, `If3`)**: Segregates applications based on credit metrics, baseline income tiering, and debt leverage ratios.
4. **Data Synchronization & Notification**: Writes final pipeline updates back to the respective sheets while triggering personalized transactional emails.

---

### 🧠 Predictive Modeling Pipeline (Orange)
Before applications enter live automation routing, risk evaluation thresholds are validated using a predictive machine learning pipeline designed in **Orange Data Mining**. This layer tests classification stability to ensure decision logic boundaries are mathematically sound.

#### Data Science Canvas
<img src="./WhatsApp Image 2026-06-11 at 13.56.30.jpeg" alt="Orange Data Mining Predictive Workflow" width="100%"/>

* **File Node**: Ingests historical credit application training profiles.
* **Select Columns**: Sets the target classification variable (`System_Initial_Decision`) and isolates key predictive features like credit score and DTI ratios.
* **Logistic Regression**: Trains a generalized linear classification model to calculate risk probabilities.
* **Test and Score**: Evaluates model accuracy, AUC-ROC statistics, and confusion matrices prior to production logic deployment.

---

### 💬 Conversational Interface (FinAssist Bot)
Applicants and clients interact directly with a front-facing AI layer via a customized web widget deployed through **Kommunicate**. 

#### Live Chat Interface Demo
<img src="./WhatsApp Image 2026-06-11 at 14.11.55.jpeg" alt="Kommunicate Chatbot Interface Demo" width="100%"/>

* **Financial Ratio Assistance**: Real-time evaluation explanations for client queries.
* **Investment Planning**: Conversational pre-screening before formal database ingestion.
* **Loan Guidance**: Guided onboarding explaining specific credit requirement criteria dynamically.

---

### 📊 Business Intelligence & Analytics Dashboard (Power BI)
To monitor the health of the lending portfolio and analyze application trends, a dedicated **Power BI Desktop** dashboard processes the workflow output data. This interactive reporting layer helps risk officers identify bottlenecks and drill down into specific rejection reasons.

#### Live Executive Analytics Canvas
<img src="./Screenshot (31).png" alt="Power BI Credit Risk Analytics Dashboard" width="100%"/>

* **High-Level KPIs**: Real-time counters showing total application volume (22 total applications in the current slice), combined portfolio asset pool values ($1M$ Total Income, $489K$ Total Loans requested), and global risk averages (614.55 Average Credit Score).
* **Application Status Distribution**: A multi-colored donut chart mapping the breakdown of automated results (`Auto_Reject`, `Auto_Approve`, `Manual_Review`).
* **Risk Segment Slicers**: Interactive filtering panels to isolate files by Status (*Rejected*), Risk Level (*High Risk*), or granular flags like *Low Income* and *Low Credit Score*.

---

### 🗂️ Dataset Structure (Google Sheets)
The underlying decision logic evaluates financial metrics across multiple columns to flag anomalies, compliance warnings, or immediate rejections.

#### Input Data Profile
<img src="./Screenshot (19).png" alt="Google Sheets Application Database" width="100%"/>

| Column Name | Description | Key Target Thresholds Evaluated |
| :--- | :--- | :--- |
| `Annual_Income` | Total gross yearly earnings | Evaluated for low-income tier audits |
| `Credit_Score` | Creditworthiness score (300 - 850) | Triggers `FAIL_CRITICAL_CREDIT` if under floor limits |
| `Debt_To_Income_Ratio` | Monthly debt obligations vs income ratio | Triggers ceiling violations if excessively high |
| `Watchlist_Match` | Compliance / AML background database matching | High percentages force automated rejection |
| `Decision_Primary_Basis` | The core automated system flag generated | e.g., `PASSED_ALL_RISK_FILTERS`, `TRIGGER_LOW_INCOME_TIER_AUDIT` |

---

### 📧 Automated Outputs & Notifications
When an application fails to meet base-level validation criteria (such as falling below standard income minimums), the workflow automatically maps the user's contact information and handles immediate email dispatching.

#### Example: Automated Reject Notification
<img src="./Screenshot (39).png" alt="Automated Gmail Reject Email via n8n" width="100%"/>

> **Automated Rejection Log Entry:**
> * **Triggering Node**: `Send a message`
> * **Reason Parsed**: `Income is low`
> * **System Footer Signature**: *This email was sent automatically with n8n*

---

## 📑 Module 2: Intelligent Invoice Parsing & Data Extraction

An autonomous data extraction solution utilizing **Nanonets AI Agents** to process unstructured commercial documents (PDF invoices) and normalize the content into standardized, tabular relational outputs for ERP or accounting ledger ingestion.

### 🤖 Document AI Parsing Engine (Nanonets)
The system leverages zero-shot deep learning OCR blocks to run deep structure analysis on unstructured data. It isolates transactional metadata fields along with complex tabular line-item details completely automatically.

#### AI Agent Extraction Interface
<img src="./Screenshot (22).png" alt="Nanonets AI Agents Invoice Parsing Interface" width="100%"/>

* **Document Intake**: Ingests multi-page raw supplier invoices (e.g., `demo-onv1.pdf`).
* **Line-Item Mappings**: Extracts descriptions, quantities, unit prices, and row totals for nested lists (e.g., *Chilled Poultry Fillets*, *Organic Fresh Spinach*, *Loaves of Whole Grain Bread*).
* **Automated Confidence Scores**: Flags low-confidence extractions for human-in-the-loop validation, while auto-approving clear items.

---

### 🧾 Structured Ledger Export (Excel/ERP Ingestion)
Once finalized by the Nanonets extraction model, data is output to an optimized structured relational sheet (`data_export_*.xlsx`) containing clean Key-Value records ready for database mapping.

#### Ledger Data Structure View
<img src="./Screenshot (23).png" alt="Excel Export of Extracted Invoice Fields" width="100%"/>

* **Invoice Details**: Captures operational references including Invoice Number (`USF-INV-10234`), Terms (`NET 30`), Purchase Order (`CK-23-4567-FB`), and Ticket Numbers.
* **Financial Calculations**: Validates invoice math automatically across Subtotal (`957.5`), Tax (`76.6`), Shipping (`50`), and Grand Total (`1084.1`) fields.
* **Corporate Entity Resolution**: Isolates corporate identities including Buyer Name (`Cloud Kitchens`), Contact Person (`Emily Chen`), Tax IDs, and physical billing addresses.

---

## ⚙️ How to Set Up & Configure

### Prerequisites
* A running instance of **n8n** (Self-hosted or Cloud).
* Active account on **Nanonets** with an API key generated for the Invoice Model.
* **Power BI Desktop** client to view and modify data model relationships (`.pbix`).
* **Orange Data Mining** desktop client (for running or adjusting the predictive `.ows` workflow).
* A **Kommunicate** account for managing live web widget interactions and conversational scripts.
* Google Workspace Account with **Google Sheets API** and **Gmail API** scopes configured via OAuth2 credentials.

### Configuration Steps
1. **Model Evaluation**: Open the Orange workflow file, point the `File` node to your evaluation dataset, and verify model scoring weights.
2. **Setup Chat Widget**: Deploy the script code provided by the Kommunicate portal into your web application to embed `FinAssist Bot`.
3. **Configure IDP Parser**: Upload sample documents to your Nanonets Invoice Agent, define the custom labels matching the fields shown in the ledger table, and activate the webhook export link.
4. **Import Workflow**: Copy the JSON representation of the n8n workflow and paste it directly into your n8n canvas interface.
5. **Link Power BI**: Open the tracking file, refresh the web-source parameters using your specific Google Sheet URL connection endpoint, and hit **Refresh Data**.
6. **Deploy**: Set the workflow toggle from **Inactive** to **Active** to begin automated production routing.
