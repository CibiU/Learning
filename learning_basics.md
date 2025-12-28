# System Integration Basics

Modern businesses use multiple software systems that must share data to run smoothly. Common examples include connecting an ERP (Enterprise Resource Planning) system with a CRM (Customer Relationship Management) platform, marketing automation, ecommerce, and finance tools. Below are the most common ways systems communicate.

## 1. APIs (Application Programming Interfaces)
APIs let software systems request and exchange data in real time using standardized endpoints.

**How it works:**
- System A sends a request (e.g., `GET /customers/123`) to System B.
- System B responds with data in a structured format (often JSON).

**Business example:**
- A CRM like Salesforce calls the ERP’s API to pull current inventory and pricing when a sales rep creates a quote.

**Best for:**
- Real-time data sharing
- On-demand queries
- Transactional workflows

## APIs in Simple Terms (Invoice Processing Example)
APIs are like a menu and messenger between systems. One system asks for something (a request), and the other system answers (a response).

**Requests and responses**
- A finance system sends a request to an ERP to create an invoice.
- The ERP returns a response confirming the invoice number and status.

**Authentication**
- The finance system must prove who it is (for example, with an API key or token) before the ERP accepts the request.

**Rate limits**
- The ERP may limit how many invoice requests can be sent per minute to prevent overload.

**Example flow**
1. Finance system sends `POST /invoices` with invoice details.
2. ERP returns `201 Created` with an invoice ID.
3. Finance system stores the ID and uses it for status checks or payment matching.

## 2. Webhooks
Webhooks are event-driven notifications. Instead of System A asking for updates, System B sends a message when something changes.

**How it works:**
- System B posts a message to a URL provided by System A whenever a specific event occurs.

**Business example:**
- An ecommerce platform sends a webhook to the ERP when a new order is placed, triggering fulfillment.

**Best for:**
- Real-time alerts
- Event-driven automation
- Reducing unnecessary polling

## 3. File-Based Exchange (CSV, XML, etc.)
Systems can exchange data through scheduled file imports and exports, often using shared folders, SFTP, or cloud storage.

**How it works:**
- System A exports a file (e.g., CSV) on a schedule.
- System B imports and processes the file.

**Business example:**
- A payroll system uploads a CSV of employee hours to a finance system nightly for reconciliation.

**Best for:**
- Batch processing
- Legacy systems without APIs
- Large data transfers on a schedule

## 4. Database Integration
Some integrations directly read from or write to another system’s database, usually through replication or ETL (Extract, Transform, Load) tools.

**How it works:**
- An ETL tool pulls data from System A’s database, transforms it, and loads it into System B’s database or data warehouse.

**Business example:**
- A BI tool extracts data from ERP and CRM databases nightly to create executive dashboards.
- A supply chain planning system loads historical sales and inventory data from the ERP database to generate demand forecasts.

**Best for:**
- Reporting and analytics
- Large-scale data consolidation
- Historical data analysis

## Choosing the Right Integration Method
A typical business uses a mix of these approaches depending on the use case:
- **APIs** for real-time access
- **Webhooks** for event-driven updates
- **Files** for batch and legacy integration
- **Databases** for analytics and reporting

By combining these methods, organizations can ensure their ERP, CRM, and other systems stay aligned and deliver consistent, accurate data across the business.

## Where Integrations Commonly Fail and Humans Are Still Needed
Even with modern integration tooling, most organizations still rely on people for exception handling, reconciliation, and governance. Below are common failure points and where human involvement remains critical.

### Common Failure Points
- **APIs:** schema changes, authentication failures, rate limits, and timeouts can break real-time data flows.
- **Webhooks:** events can be missed or duplicated if endpoints are down or retries are not idempotent.
- **File exchange:** format changes, missing headers, or manual edits can cause imports to fail or skip data.
- **Database/ETL:** stale data windows, transformation errors, or access restrictions can lead to incorrect reporting.

### Where Humans Are Still Used Today
- **Reconciliation and audits:** finance teams compare ERP, CRM, and payment data to resolve mismatches.
- **Approval workflows:** credits, refunds, and purchasing often require human sign-off.
- **Data quality fixes:** analysts correct mappings or clean source data after upstream changes.
- **Monitoring and recovery:** integration teams replay failed jobs or resubmit webhook events.

<h2 style="font-size: 2.2em;">Common Business Data Formats and Why Unstructured Data Is Hard</h2>
Business workflows rely on consistent formats so systems can validate and map fields reliably.

**Common structured and semi-structured formats**
- **CSV:** common for payroll exports, inventory lists, and batch updates.
- **XML:** a tag-based markup format often used in legacy systems, EDI-style exchanges, and some ERP integrations.
- **JSON:** a lightweight, key-value format commonly used in modern APIs and webhooks.
- **EDI (e.g., X12, EDIFACT):** a standardized business document format for supply chain messages like purchase orders and invoices.
- **Spreadsheets (XLSX):** common for manual handoffs, but still structured.

**Why unstructured data is hard**
- **Ambiguity:** emails, PDFs, and free-form text lack consistent fields.
- **Extraction errors:** OCR and text parsing can misread values like amounts or dates.
- **Inconsistent layouts:** the same vendor may change invoice templates over time.
- **Higher validation effort:** humans must confirm meaning and accuracy before posting to ERP/CRM.
