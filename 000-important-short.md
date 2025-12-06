## 1️⃣ Maintain a data analytics solution (Governance, Admin, Lifecycle)

Ei part mainly 4টা জিনিস নিয়ে:

1. **Security & governance (access, RLS/CLS/OLS, sensitivity, endorsement)**
2. **Admin: workspaces, capacities, roles**
3. **Dev lifecycle: Git, PBIP, deployment pipelines**
4. **Monitoring & impact analysis**

---

### 1.1 Security & access control in Fabric

**a) Workspace-level access**

Roles:

* **Admin** – সবকিছু, settings change, delete, access manage
* **Member / Contributor** – create/edit items (Lakehouse, Dataflow, Reports, Pipelines)
* **Viewer** – শুধু দেখতে পারবে, change করতে পারবে না

👉 **Exam pattern:**
*“User can open report but can’t edit or publish new dataflows”* → role probably **Viewer**, but needs at least **Contributor**.

---

**b) Item-level permissions**

Every item (Lakehouse, Warehouse, Semantic model, Report) has **own permissions**:

* A user workspace e Contributor hote pare, but **semantic model e Build nai** → new report/create from that model possible na.

Key keyword: **Build permission**

* লাগে:

  * Analyze in Excel
  * New report from that dataset
  * Semantic model reuse across workspace

---

**c) RLS / CLS / OLS / file-level control** ([learn.microsoft.com][1])

* **RLS (Row-Level Security)** → kon user kon row dekhbe (e.g., Country = ‘BD’ only)
* **CLS / Column-level security** → কিছু sensitive column hide (e.g., Salary)
* **OLS (Object-level security)** → পুরো table hide
* **File-level security** → OneLake / Files folder e access control (especially Lakehouse Files)

**Fabric angle:**

* Lakehouse / Warehouse table → RLS with security roles (semantic model e)
* Files access → আলাদা filesystem permission (OneLake) – অনেক question এখান থেকে আসবে

---

**d) Sensitivity labels (Purview)** ([learn.microsoft.com][1])

Labels like:

* Public
* General
* Confidential
* Highly confidential – No export

Impact:

* Export to Excel / CSV blocked
* Publish to web blocked
* External share blocked (encrypted label হলে)

Important settings:

* **Allow users to apply sensitivity labels**
* **Automatically apply labels to downstream content**
* **Allow Purview to secure AI interactions** (Copilot + labels)

Exam pattern:

> “User can view the report, but export is blocked after applying label.”
> → Label configuration, likely **No Export**.

---

**e) Endorsement: Promoted / Certified**

* **Promoted** – team level confidence
* **Certified** – org-level, governed source of truth
* Often discoverable via “Data hub / OneLake / Explorer”.

Exam question:

> “Central team wants to mark some semantic models as trusted and visible to whole org.”
> → Use **Certification** with proper admin policy.

---

### 1.2 Admin & governance: tenant, capacity, workspace

Short summary:

* **Tenant** → ORG-wide policy (Fabric on/off, export, trial, guest, labels). ([learn.microsoft.com][1])
* **Capacity** → Compute (Spark, DirectLake, Pipelines). ([learn.microsoft.com][2])
* **Workspace** → Team scope, assigned to a capacity.

Exam-type topics:

* Shared vs Fabric capacity
* “Users can create Fabric items”
* Guest users can access Fabric
* Export/Download settings
* Publish to web on/off
* Capacity paused, Spark limits, queue

We already did MANY questions on this; eta tomar **admin section**.

---

### 1.3 Analytics development lifecycle (CI/CD, versioning)

Skills area: **“Maintain the analytics development lifecycle”** ([learn.microsoft.com][1])

Key parts:

#### a) Version control with Git

* Fabric workspace ke **Git repo** er sathe connect kora jai:

  * Reports as **PBIP/PBIR**
  * Notebooks as files
  * SQL scripts, Data pipelines definitions etc.

Why important:

* Team collaboration
* Pull request workflow
* Track changes

---

#### b) PBIP (.pbip) / PBIR structure

* **PBIP / PBIR** = text-based structure; easier for Git & DevOps.
* DP-600: বুঝতে হবে difference between PBIX vs PBIP/PBIR.

---

#### c) Deployment pipelines

* Typically: **Dev → Test → Prod**

* Can deploy:

  * Lakehouse / Warehouse?
  * Semantic models
  * Reports
  * Dataflows (in some scenarios – exam may mention XMLA)

* Important ideas:

  * **Rules** (parameter override per stage)
  * Data source bindings
  * Testing in Test before Prod

---

#### d) XMLA endpoint (for semantic models) ([learn.microsoft.com][1])

* Enterprise model management: partitioning, scripted deployment, external tools (Tabular Editor, SSMS).
* DP-600 expects conceptual: what can you do via XMLA – manage semantic models at enterprise scale.

---

#### e) Impact analysis

Skills bullet: “Perform impact analysis of downstream dependencies” ([learn.microsoft.com][1])

* Use **Lineage view** / impact analysis tools:

  * If you change a Lakehouse table
  * Which Dataflows, semantic models, reports are impacted
* Very exam-ish scenario:

  > “Before changing schema of table, how to see which downstream reports will be affected?”

---

## 2️⃣ Prepare data (largest part, most marks) ([Promethium][3])

Eta holo **DP-600 er হৃৎপিণ্ড** – ETL / ELT / Lakehouse / Warehouse / Dataflows / Pipelines.

Breakdown:

1. **Ingest data → connectors, Data Factory, shortcuts**
2. **Transform data → Dataflows Gen2, Spark, T-SQL**
3. **Store/serve → Lakehouse, Warehouse, KQL DB**
4. **Patterns → Incremental, CDC, batch vs streaming**
5. **Data quality & business rules**

---

### 2.1 Ingest data into Fabric

**Tools:**

* **Data Factory (Fabric Data Factory experience)**

  * Copy Activity
  * Pipeline templates
  * 300+ connectors (SQL, Blob, ADLS, Salesforce, etc.) ([Promethium][3])

* **Dataflow Gen2**

  * Power Query online
  * M-language based transformations
  * Destinations: Lakehouse, Warehouse, KQL DB

* **Spark Notebooks**

  * PySpark/Scala to load data from sources
  * Write to Delta Tables in Lakehouse

* **Shortcuts (zero-copy)**

  * Point to data in ADLS Gen2 / AWS S3 / Azure OneLake
  * No copy needed.

---

### 2.2 Transform data

**Three main engines:**

1. **Dataflow Gen2 (Power Query)**

   * GUI-based transformation
   * Ideal for business-friendly ETL
   * Good for dimension/fact building, simple cleansing.

2. **Spark Notebooks (Data Engineering)**

   * Big data transformations
   * Complex joins, heavy compute
   * Streaming + batch both.

3. **T-SQL (Warehouse / SQL Endpoint)**

   * ELT style: load raw → transform inside Warehouse using SQL
   * Stored procedures, views etc.

Exam e আসবে:

* কখন Dataflow, কখন Spark, কখন T-SQL use korbe (scenario ভিত্তিক choice)
* Star-schema / dimension-fact design concepts

---

### 2.3 Lakehouse & Warehouse

**Lakehouse:**

* Files + Tables (Delta)
* Ideal for raw + medallion architecture (Bronze/Silver/Gold).
* Used with Spark + DirectLake.
* Good for big data, semi-structured.

**Warehouse:**

* SQL-first view; structured tables
* Strong T-SQL support
* Typically **Gold layer** / conformed data.
* Works nicely with semantic model directly.

Exam scenario:

> “Customer 360 view, heavy structured reporting, finance team, strong T-SQL skills → choose Warehouse.”
> Versus
> “Big data, logs, events → Lakehouse + Spark.”

---

### 2.4 Patterns: incremental, CDC, real-time

* **Incremental load**

  * Only process new/changed data
  * Dataflow incremental policy
  * SQL-based watermarks (LastModifiedDate etc.)

* **CDC (Change Data Capture) / change feed**

  * Transaction log based; only changed rows.
  * Combined with Warehouse or other store.

* **Real-time / streaming** (DP-600 now touches a bit on Real-Time Intelligence) ([Promethium][3])

  * Eventstreams
  * KQL DB
  * Real-time dashboards.

---

## 3️⃣ Implement and manage semantic models ([learn.microsoft.com][1])

This is basically **Power BI modeling + Fabric integration**:

1. Model types & storage modes
2. Star schema design
3. Relationships
4. DAX basics
5. Performance & optimization
6. Security (RLS/OLS) at model level

---

### 3.1 Storage modes: Import, DirectQuery, DirectLake, Composite

* **Import** – Data cached in model; fast; needs refresh.
* **DirectQuery** – Query source live; slower; no full cache.
* **DirectLake** – Fabric-only; queries Delta tables directly from OneLake with cached optimizations.
* **Composite** – Mix of Import + DirectQuery + DirectLake.

Exam e scenario:

> “Fabric Lakehouse + very large data + low latency required + Fabric capacity available” → DirectLake.

---

### 3.2 Modeling fundamentals

* **Star schema**:

  * Fact tables (transactions)
  * Dimension tables (customers, products, dates etc.)

* **Relationships**:

  * One-to-many (most common)
  * Many-to-many (use with caution)
  * Single / both-direction.

* **Best practices**:

  * Avoid snowflake if possible for performance
  * Use surrogate keys
  * Filter direction carefully.

---

### 3.3 DAX & calculations

Key DAX concepts:

* **Calculated columns vs Measures**
* **Row context vs Filter context**
* **Time intelligence** (TOTALYTD, SAMEPERIODLASTYEAR)

DP-600 e heavy DAX deep dive na, but:

* তুমি basic time calculations, filter based logic, context transition concept bujle safe.

---

### 3.4 Security in semantic models

* **RLS** – role-based row filter

* **OLS** – hide specific columns/tables

* RLS enforces:

  * Even if user has Build, they still see only allowed rows.

* Works with:

  * Import
  * DirectQuery
  * DirectLake (with some nuances, but conceptually yes).

---

### 3.5 Performance & optimization

* Large models → need:

  * Proper relationships
  * Avoid bi-directional filters unnecessarily
  * Use aggregations
  * Use calculation groups (tabular editor)
  * Partitioning (via XMLA for enterprise)

* DP-600 expects conceptual knowledge:
  *“What to do if model is slow?”* → star schema, summarise, measure optimization, avoid heavy row context loops.

---

## 🎓 How I suggest you study (practical plan)

Since tumi already admin / Dataflow practice kortecho, ami eta recommend korbo:

### Step 1 – Foundations (Fabric & objects)

* Fabric items: Lakehouse, Warehouse, Dataflow Gen2, Pipeline, Notebook, Semantic model, KQL DB.
* Lakehouse vs Warehouse vs KQL DB.

### Step 2 – Prepare data (Hands-on + theory)

* Dataflow Gen2: connect → transform → load to Lakehouse
* Pipeline: run Dataflow + Notebook chain
* Lakehouse tables & Delta basics
* Shortcuts

### Step 3 – Semantic model & reporting

* Create model from Lakehouse
* Use DirectLake & Import; understand difference
* RLS on semantic model
* Simple DAX (SUM, CALCULATE, FILTER, time-intel basic)

### Step 4 – Admin & governance

* Tenant vs capacity vs workspace
* Export/sharing policies
* Sensitivity labels & guest access
* Deployment pipelines & Git

---

## ✅ Next: which topic you want explained DEEP first?

I can take **one big block**, and teach it like a mini-course with:

* Concept
* Simple analogy in Bangla
* Fabric UI path
* Likely exam question pattern
* 3–5 practice questions

For example, you can say:

* **“Prepare data topic ta deep shikhaw”**
  or
* **“Semantic model + DirectLake topic ta bistarito chai”**
  or
* **“RLS / security part ta deep e chai”**



[1]: https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/dp-600?utm_source=chatgpt.com "Study guide for Exam DP-600: Implementing Analytics ..."
[2]: https://learn.microsoft.com/en-us/training/courses/dp-600t00?utm_source=chatgpt.com "Course DP-600T00-A: Microsoft Fabric Analytics Engineer"
[3]: https://promethium.ai/guides/microsoft-fabric-certification-guide-dp600-dp700/?utm_source=chatgpt.com "Microsoft Fabric Certification Guide: DP-600 & DP-700 Exam ..."
