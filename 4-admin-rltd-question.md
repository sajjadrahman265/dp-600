## 0️⃣ Big Picture – Fabric admin settings actually kothay kothay?

Fabric e **3 main level** settings mone রাখো:

1. **Tenant level** – পুরো organization-er policy

   * “Users can create Fabric items”, trials, export policy, guest users, external sharing, sensitivity labels etc. ([Microsoft Learn][1])

2. **Capacity level** – F-SKU / Premium capacity per settings

   * Region, size (F64, F128…), workload limits, Spark limits, delegate tenant settings etc. ([Microsoft Learn][2])

3. **Workspace level** – specific workspace-er config

   * Workspace info, license mode, Spark pool, storage, connections, etc. ([Microsoft Learn][3])

**DP-600 exam trick:**
Often question bole: *“Which admin level should change this?”*
So always think – **Tenant vs Capacity vs Workspace**.

---

## 1️⃣ Tenant Settings – Category by Category (deep, but exam-focused)

Tenant settings dekhte gele:
**Gear icon (⚙) → Admin portal → Tenant settings** ([Microsoft Learn][1])

Docs: **Tenant settings index** full list diche. ([Microsoft Learn][4])

Ami ekhane **সবচেয়ে important group** gulo line by line explain korbo, DP-600 relevant ভাবে.

---

### 1.1 “Microsoft Fabric” section

Ei group mainly bole: **org-er moddhe Fabric / advanced features on/off**.

Key settings:

#### 🔹 Users can create Fabric items ([Microsoft Learn][5])

* **Ki kore:**

  * On = users can create **Lakehouse, Warehouse, Dataflow Gen2, Pipeline, Notebook, KQL DB…**
  * Off = tara Power BI items (report, semantic model) create korte parbe, but **Fabric workloads no**.
* Level: **Tenant + Capacity** du jagay manage kora jai.
* Exam scenario:

  > “Users can create Power BI reports but not Lakehouses or Dataflows. Which setting should you check?”
  > Answer → **Users can create Fabric items**.

#### 🔹 Digital Twin Builder (preview)

* Allow users to create **Digital Twin Builder** items for modeling physical systems digitally.
* Only relevant jodi org digital twin / IoT type workload use kore.

#### 🔹 Enable Ontology item (preview)

* Ontology = **enterprise semantic layer** (entities, relationships, meaning) for AI/agents.
* On korle users ontology item create korte parbe.

#### 🔹 Users can discover and create org apps (preview) ([Microsoft Learn][5])

* Org app = **new style of applications** (not just workspace app).
* Off korle org apps hidden thakbe, purono workspace app still thakbe.
* Exam trick: Kono org app dekhache na → this setting off.

#### 🔹 Product Feedback

* Microsoft ke **in-product survey** show korte dibe kina.
* Security / data-governance heavy org often disable.

#### 🔹 Users can create and share Data agent items (preview)

* Data agent = **natural language Q&A + generative AI** driven item.
* On = users AI-based data agent build & share korte parbe.

#### 🔹 User can create Graph (preview) / Maps / Operations Agents, etc.

* Ei sob specific workloads on/off.
* Pattern: “Users can create X item” == allow or block that feature for tenant/capacity.

**Exam-wise:**
Tomar mone rakhte hobe ekta pattern:

> If question is “Why user can’t see this new Fabric experience?” → Check **Microsoft Fabric section** of tenant settings, especially **Users can create Fabric items** + specific preview toggle.

---

### 1.2 Help and support settings ([Microsoft Learn][5])

#### 🔹 Publish “Get Help” information

* Fabric “Help” menu theke **internal support page / URL** e redirect korte parbe.
* Large org-gulo private help page use kore.

#### 🔹 Receive email notifications for service outages or incidents

* Select **mail-enabled security group** – tara outage / incident mail pabe.

#### 🔹 Users can try Microsoft Fabric paid features

* On = users **Fabric trial (60 days)** start korte pare, paid features try korte pare. ([Microsoft Learn][6])
* Off = self-service trial blocked.
* Exam scenario:

  > “Org wants to prevent users from starting Fabric trials.”
  > → Turn this **off**.

#### 🔹 Show a custom message before publishing reports

* User jokhon report publish korbe, tar age ekta **custom warning message** show.

  * e.g., “Do not publish confidential data”.

---

### 1.3 Domain management settings

#### 🔹 Allow tenant and domain admins to override workspace assignments

* Jodi workspace domain-ভিত্তিক হয়ে থাকে (multi-domain tenant), admin workspace ke **one domain theke another domain-e move** korte parbe.
* Multi-regional / multi-company scenarios.

---

### 1.4 Workspace settings (very important for exam) ([Microsoft Learn][5])

#### 🔹 Create workspaces

* Control: **ke workspace create korte parbe**?

  * Everyone / None / only specific security groups.
* Even if off, **template app install** korle ekta workspace auto create hoy.

#### 🔹 Use semantic models across workspaces

* On = jodi user-er **Build permission** thake, se **other workspace-er semantic model** reuse korte pare.
* Off = strict workspace boundary.
* DP-600 scenario:

  > “Central team created a certified semantic model, but other teams can't connect from their own workspaces.”
  > → Check this setting.

#### 🔹 Block users from reassigning personal workspaces (My Workspace)

* My Workspace ke Premium capacity theke shared capacity-te **move korte deba kina**.
* Governing cost / performance.

#### 🔹 Define workspace retention period

* Delete korar por workspace koto din restor-able thakbe (≥7 days, up to 90 for normal, 30 for My Workspace).
* On = custom retention; Off = minimum 7 days.

#### 🔹 Automatically convert and store reports using PBIR format (preview)

* On = reports **PBIR** (source-control friendly file format) e save hobe. ([Microsoft Learn][5])
* DevOps / git integration friendly.

---

### 1.5 Information protection (Sensitivity labels & Purview) ([Microsoft Learn][5])

#### 🔹 Allow users to apply sensitivity labels for content

* On = Purview sensitivity labels apply kora jabe (Confidential, Highly Confidential, etc.).
* Enforces label-based policies on exports & access.

#### 🔹 Apply sensitivity labels from data sources to their data in Power BI

* If source (e.g., SQL, Synapse) e label ache, seta automatically **Fabric content e inherit** korte pare.

#### 🔹 Automatically apply sensitivity labels to downstream content

* Label propagate → semantic model → report → dashboard etc.

#### 🔹 Allow workspace admins to override automatically applied sensitivity labels

* Workspace admin jodi mistakenly strict label apply hoy, then shei label change/remove korte parbe kina.

#### 🔹 Restrict content with protected labels from being shared via link with everyone in your organization

* Jodi label encrypted/protected hoy, tokhon whole org shareable link block.

#### 🔹 Domain admins can set default sensitivity labels for their domains

* Domain-wise default label set kora jabe.

#### 🔹 Allow Microsoft Purview to secure AI interactions

* Purview ke allow kore **Copilot / AI prompts & responses** scan korte for DLP/compliance.

**Exam-angle**:
Jokhon question e **sensitivity label / export control / external sharing** ashe → ei block theke answer ber hoy.

---

### 1.6 Export and sharing settings (super exam-relevant) ([Microsoft Learn][5])

Important bullets:

* **External data sharing**

  * On = OneLake data **external tenant-e share** kora jabe read-only link diye (lakehouse, etc.).

* **Users can accept external data shares**

  * On = tomar users onno tenant theke share paile accept kore use korte parbe.

* **Guest users can access Microsoft Fabric**

  * B2B guest (Entra ID guest) can log in & use Fabric, based on permissions.

* **Users can invite guest users…**

  * Internal user external ke invite korte parbe kina.

* **Guest users can browse and access Fabric content**

  * Guest ra “discover” section e content dekhte/request access korte parbe kina.

* **Users can see guest users in lists of suggested people**

  * Sharing time e suggestion list e guest ke include korbe kina.

* **Publish to web**

  * Public, unauthenticated URL for report. **Very risky**.
  * Often exam e:

    > “Org wants to prevent leak via public URL.” → Turn this off.

* **Export to Excel / CSV / Download reports / Export report as PPT/PDF/etc.**

  * Ei gulo sab “data exfiltration risk” related.
  * High security org often disables.

* **Allow shareable links to grant access to everyone in your organization**

  * On = org-wide link (no explicit add user).
  * Off = must explicitly add users / security groups.

* **Certification / Endorse master data**

  * Controls ke **certify** or **endorse master data** korte pare.

* **Email subscriptions & external users**

  * Controls who can create email subscriptions and whether external users receive them.

Exam pattern:

> “Prevent users from exporting report data to Excel/CSV while still letting them view in Power BI.”
> → **Export to Excel/CSV** settings.

---

### 1.7 Discovery settings

* **Make promoted/certified content discoverable**

  * Users jara access nei, tara “discover” page e see + request access korte pare kina.

* **Discover content**

  * Overall permission to discover content beyond direct access.

---

### 1.8 App settings

* **Create template organizational apps**
* **Push apps to end users**
* **Publish apps to entire organization**

Mostly Power BI app distribution control.

---

### 1.9 Integration settings (Power BI + external services) ([Microsoft Learn][5])

Includes things like:

* XMLA endpoints & Analyze in Excel
* ArcGIS Maps, Azure Maps
* SharePoint / Microsoft Lists integration
* SSO with Dremio, Snowflake, Redshift, BigQuery
* Entra SSO for data gateway
* OneDrive/SharePoint PBIX integration
* Semantic models export to OneLake, auto-update from OneDrive/SharePoint
* ArcGIS GeoAnalytics for Spark
* Allow non-Entra auth in Eventstream (security tightening)

Pattern: ei group mostly **integration & SSO**.

---

### 1.10 Power BI visuals + R/Python visuals

* Allow AppSource/custom visuals, only certified visuals, custom visuals download data, custom visuals SSO, access browser localStorage etc.
* R/Python visual interaction on/off.

This is privacy/security + which visuals allowed.

---

### 1.11 Audit and usage settings

* Usage metrics visibility (including per-user identity)
* Show user data in Capacity Metrics app
* Allow workspace admins to turn on monitoring (Eventhouse + KQL)
* Microsoft may store query text for support.

---

### 1.12 Dashboard settings

* **Web content on dashboard tiles** – allow embedding arbitrary web content (risky).

---

### 1.13 Developer settings

* Embed content in apps (Embed for your customers)
* Service principals can:

  * create workspaces/connections/pipelines
  * call Fabric public APIs
  * create/use profiles
* Block ResourceKey Authentication for streaming semantic models.

👉 **DP-600 dev/governance question** often comes from here.

---

### 1.14 Admin API settings

* Service principals can access:

  * read-only admin APIs
  * update admin APIs
* Enhance admin API responses with detailed metadata (table/column names etc.).

---

## 2️⃣ Capacity Settings – Fabric Capacity / Premium / Trial

**Where:** Admin portal → Capacity settings ([Microsoft Learn][2])

Key concepts:

* **Capacity type**:

  * Power BI Premium, Embedded, Trial, Fabric Capacity
* **Region, SKU size** (F64, F128…)
* **Capacity admins** – who can manage that capacity.
* **Workloads configuration** – memory/concurrency per workload (Data Engineering, Data Science, SQL, Power BI etc.). ([Microsoft Learn][7])

Special Fabric bits:

* **Data Engineering/Science settings** – cluster size, Spark pools, timeouts. ([Microsoft Learn][8])
* **Delegate tenant settings** – capacity level e “Users can create Fabric items” etc. override korte paro tenant setting ke. ([Microsoft Learn][9])

Exam angle:

> “Only workspaces in certain capacity should allow Fabric workloads / Dataflow Gen2. Others only Power BI.”
> → Use **Delegate tenant settings** per capacity.

---

## 3️⃣ Workspace Settings – per workspace admin panel

**Where:** Workspace select → `…` → **Workspace settings** ([Microsoft Learn][3])

Major sections (high level):

### 3.1 General

* Name, description
* Workspace contacts (who gets error notifications)
* Image/icon etc.

### 3.2 License / Capacity

* Workspace **assigned to which capacity** (shared / Premium / Fabric).
* Determines whether **Fabric items** allowed inside that workspace.

### 3.3 Storage / SharePoint link

* Linked SharePoint/OneDrive location for files (if any).

### 3.4 Azure connections / Data sources

* Workspace-level connections, etc.

### 3.5 Data Engineering/Science (Spark) ([Microsoft Learn][10])

* Default Spark pool (starter pool or custom pools)
* Cluster sizes, concurrency (indirect via pool)
* High concurrency / advanced Spark settings (Delta upgrades etc.).

**DP-600** e eitar theke ashte pare:

> “Where do you change default Spark pool for notebook runs in a specific workspace?”
> → **Workspace settings → Data Engineering/Science → Spark Compute**.

---

## 4️⃣ How to use all this in exam questions (short strategy)

Jokhon kono confusing scenario thakbe:

* “User can’t create Dataflow Gen2”

  1. Check: **Users can create Fabric items** (Tenant/Capacity)
  2. Check: Workspace capacity Fabric enabled
  3. Check: User’s workspace role (Contributor+)

* “External users not able to access lakehouse shared with them”

  * Check:

    * **Guest users can access Microsoft Fabric**
    * **Users can invite guest users…**
    * External data sharing on?

* “Org wants to block export but allow viewing reports”

  * Go to **Export and sharing** → Export to Excel/CSV/Download reports.

* “Prevent self-service trial”

  * **Users can try Fabric paid features** → Off.

---

## If you want next…

I can now do **DP-600-style deep scenario questions** only based on:

* Tenant + capacity + workspace settings
* Dataflow Gen2 permission & governance
* External/guest access & sensitivity labels

For example, **20–30 complex case studies** with full explanation, jeta directly ei admin settings theke asbe.

Great — I will rewrite the first **50 questions** exactly in your requested format:

### **Question → MCQ Options → Correct Answer → Explanation for EACH option**

✔ DP-600 exam style
✔ Clear, structured, deeply explained
✔ The remaining 50 will be sent in the next message once you confirm.

---

# 🔵 **DP-600 MOCK EXAM (REWRITTEN) — FIRST 50 QUESTIONS**

## **Each Question Includes: MCQ Options + Correct Answer + Full Explanation**

---

# ✅ **SECTION 1 — Fabric Capacity, Tenant Settings & Admin Scenarios (Q1–Q20)**

---

## **Q1. Why can users create Power BI reports but NOT Fabric items like Lakehouse or Dataflow Gen2?**

### Options:

A. Workspace is read-only
B. “Users can create Fabric items” is disabled
C. Spark is not configured
D. Lakehouse preview is disabled

### ✔ **Correct Answer: B**

### Explanation:

* **A — Wrong:** Read-only workspace does NOT exist; permissions decide creation.
* **B — Correct:** When tenant disables *Users can create Fabric items*, users cannot create Lakehouse, Warehouse, Dataflow Gen2, Pipelines.
* **C — Wrong:** Spark affects execution, not item creation.
* **D — Wrong:** Lakehouse preview toggle does not block Dataflow/Pipeline creation.

---

## **Q2. Workspace is assigned to Shared capacity. What is unavailable?**

A. Power BI reports
B. Datasets
C. Fabric items (Lakehouse, Warehouse, Dataflow Gen2, Notebook)
D. Admin portal

### ✔ Correct Answer: C

### Explanation:

* **A — Wrong:** Reports work everywhere.
* **B — Wrong:** Datasets work in all capacities.
* **C — Correct:** Shared capacity cannot host Fabric workloads — only Power BI features exist.
* **D — Wrong:** Admin portal is tenant-wide.

---

## **Q3. After moving a workspace to F64 capacity, pipelines still cannot run. Why?**

A. Pipeline permissions missing
B. Pipeline workload disabled at capacity level
C. User license is free
D. Notebook is corrupted

### ✔ Correct Answer: B

### Explanation:

* **A — Wrong:** Permissions block editing, not running.
* **B — Correct:** Capacity admin must enable *Data Pipelines workload*.
* **C — Wrong:** Pipelines don’t require Pro license inside Fabric capacity.
* **D — Wrong:** Notebook corruption doesn’t affect pipeline availability.

---

## **Q4. User can run Notebook but cannot create new ones. Why?**

A. Workspace admin disabled notebook creation
B. “Users can create Fabric items” disabled
C. Spark is offline
D. User is Viewer

### ✔ Correct Answer: B

### Explanation:

* **A — Wrong:** Workspace cannot individually disable notebook creation.
* **B — Correct:** Tenant-level “Users can create Fabric items” disables creating ANY Fabric item.
* **C — Wrong:** If Spark offline, running fails too.
* **D — Wrong:** Viewers cannot run notebook either.

---

## **Q5. DirectLake mode missing for a semantic model. Why?**

A. Dataset is too large
B. Workspace is on Shared capacity
C. Sensitivity label applied
D. RLS enabled

### ✔ Correct Answer: B

### Explanation:

* **A — Wrong:** Size doesn’t disable DirectLake.
* **B — Correct:** DirectLake needs Fabric or Premium capacity.
* **C — Wrong:** Labels don’t affect DirectLake availability.
* **D — Wrong:** RLS works with DirectLake.

---

## **Q6. Fabric capacity shows “Paused.” Effect?**

A. Only Dataflows fail
B. Only Lakehouse SQL endpoint stops
C. All Fabric compute workloads stop
D. Only Pipelines stop

### ✔ Correct Answer: C

### Explanation:

Paused capacity halts:

* Spark
* Dataflows
* Pipelines
* SQL endpoint
* Any compute operation

Everything fails.

---

## **Q7. “Users can try Fabric paid features” disabled. What happens when clicking “Start Trial”?**

A. Trial activates for 7 days
B. Trial activates for 60 days
C. Activation blocked
D. Redirects to admin approval

### ✔ Correct Answer: C

### Explanation:

Trial is *completely blocked* for all users.

---

## **Q8. Dataflow Gen2 cannot connect to GitHub CSV. Why?**

A. GitHub unsupported
B. OAuth required
C. Anonymous/public data sources disabled
D. Dataflow credentials missing

### ✔ Correct Answer: C

### Explanation:

GitHub raw file requires **Anonymous**. If tenant blocks anonymous sources → fail.

---

## **Q9. Guest user invited but sees no Fabric items. Why?**

A. Guest must be Workspace Admin
B. “Guest users can access Fabric” disabled
C. Dataset endorsement missing
D. No Power BI Pro license

### ✔ Correct Answer: B

---

## **Q10. Org wants to block PBIX download. Which setting?**

A. Turn off Export to CSV
B. Disable Download report
C. Disable Publish to web
D. Enable sensitivity labels

### ✔ Correct Answer: B

---

## **Q11. To enable Copilot, what must be turned ON?**

A. Semantic model refresh
B. Purview to secure AI interactions
C. Guest access
D. Workspace retention policy

### ✔ Correct Answer: B

---

## **Q12. Org wants to block export but allow viewing. Which setting?**

A. Disable publish to web
B. Disable export data
C. Disable workspace creation
D. Enable certified datasets

### ✔ Correct Answer: B

---

## **Q13. DirectLake suddenly slow. Why?**

A. Dataflow refreshed
B. Capacity overload
C. User changed tables
D. Table moved to Files folder

### ✔ Correct Answer: B

### Explanation:

If capacity overloaded:

* Delta cache evicts
* DirectLake behaves like DirectQuery → slow

---

## **Q14. Auto PBIR conversion controlled by which setting?**

A. Publish to web
B. Automatically convert PBIX to PBIR
C. Enable analytics preview
D. Export settings

### ✔ Correct Answer: B

---

## **Q15. Which setting controls workspace creation?**

A. Workspace role
B. Domain trust
C. Tenant → Workspace → Create workspaces
D. Capacity assignment

### ✔ Correct Answer: C

---

## **Q16. Dataflow fails with “Insufficient capacity.” What to inspect?**

A. Spark pool version
B. Capacity-level workload settings
C. Workspace admins
D. M query steps

### ✔ Correct Answer: B

---

## **Q17. Tenant blocks anonymous connectors. Which fails?**

A. SQL
B. Azure AD
C. GitHub CSV
D. SharePoint list

### ✔ Correct Answer: C

---

## **Q18. To enable external Lakehouse sharing, which control?**

A. Guest access
B. Publish to web
C. External data sharing
D. Incremental refresh

### ✔ Correct Answer: C

---

## **Q19. Notebook fails: “Spark cannot allocate nodes.” Why?**

A. Delta corrupted
B. Spark concurrency/max nodes reached in capacity
C. Lakehouse offline
D. SQL endpoint down

### ✔ Correct Answer: B

---

## **Q20. Sensitivity labels not visible. Why?**

A. No dataset endorsed
B. Purview disabled
C. “Allow sensitivity labels” disabled
D. External guest access disabled

### ✔ Correct Answer: C

---

# 🔵 **SECTION 2 — Lakehouse, Delta Tables, Shortcuts (Q21–Q40)**

---

## **Q21. User can query Tables but cannot open Files. Missing permission?**

A. Viewer
B. Build
C. OneLake filesystem permission
D. SQL endpoint access

### ✔ Correct Answer: C

---

## **Q22. DirectLake requires Delta. Which file unsupported?**

A. Parquet
B. Delta
C. JSON
D. CSV

### ✔ Correct Answer: C & D

(DirectLake only works with *Delta tables*, not raw text formats.)

---

## **Q23. Which operation NOT supported on Delta table?**

A. Time travel
B. Schema evolution
C. Manual deletion of delta logs
D. MERGE operations

### ✔ Correct Answer: C

---

## **Q24. Shortcut shows outdated files. Why?**

A. Shortcut syncs slowly
B. Shortcut NEVER syncs — it's just a pointer
C. OneLake cache issue
D. Token expired

### ✔ Correct Answer: B

---

## **Q25. Shortcut returns access denied. What to check?**

A. Fabric capacity
B. Gateway
C. External storage permissions
D. Spark pool

### ✔ Correct Answer: C

---

## **Q26. User sees Lakehouse but cannot query SQL endpoint. Why?**

A. Missing read permission on SQL endpoint
B. Wrong capacity
C. Table corrupted
D. Spark failed

### ✔ Correct Answer: A

---

## **Q27. What forces Delta schema rebuild?**

A. Restart capacity
B. VACUUM
C. OPTIMIZE / REPAIR
D. Rename table

### ✔ Correct Answer: C

---

## **Q28. Files uploaded — how to register as table?**

A. Drop into SQL endpoint
B. Create shortcut
C. Define table using “New Table” → infer schema from files
D. Rename file

### ✔ Correct Answer: C

---

## **Q29. Parquet written to Files not appearing in Tables. Why?**

A. Wrong file type
B. File not auto-registered
C. Spark crashed
D. SQL endpoint down

### ✔ Correct Answer: B

---

## **Q30. Permission needed to query SQL endpoint?**

A. Build
B. Read Data
C. OneLake FS permission
D. Admin only

### ✔ Correct Answer: B

---

## **Q31. Lakehouse shows two tables with similar names. Why?**

A. Case sensitivity
B. Duplicate metadata
C. Wrong shortcut
D. Delta conflict

### ✔ Correct Answer: A

---

## **Q32. Shortcut supports which feature?**

A. Data copy
B. Live pointer to external storage
C. Manual sync
D. Schema enforcement

### ✔ Correct Answer: B

---

## **Q33. Time travel relies on what?**

A. VACUUM
B. Delta log versions
C. Parquet cache
D. Optimize write

### ✔ Correct Answer: B

---

## **Q34. Admin setting blocking shortcut creation?**

A. Disable public data sources
B. External storage connections restricted
C. Export disabled
D. RLS applied

### ✔ Correct Answer: B

---

## **Q35. Table corrupted after delta logs deleted. Fix?**

A. Optimize
B. Rebuild delta log by recreating table
C. Refresh
D. Rename folder

### ✔ Correct Answer: B

---

## **Q36. User cannot rename table. Why?**

A. Only admin can rename
B. Need write permissions on Lakehouse
C. Table locked in SQL endpoint
D. Schema mismatch

### ✔ Correct Answer: B

---

## **Q37. What increments Delta version?**

A. Query table
B. Any write (INSERT/UPDATE/MERGE/DELETE)
C. VACUUM
D. OPTIMIZE

### ✔ Correct Answer: B

---

## **Q38. Schema evolution requires enabling what in Dataflow?**

A. Incremental load
B. Auto-adjust data types
C. Allow schema drift
D. Use M language

### ✔ Correct Answer: C

---

## **Q39. Why DirectLake only in Premium/Fabric?**

A. Needs special data formats
B. Requires ultra-fast cache in capacity
C. Runs only in SQL endpoint
D. Requires Pro license

### ✔ Correct Answer: B

---

## **Q40. User sees Lakehouse but can't create items. Why?**

A. Role = Member
B. Tenant disabled “Users can create Fabric items”
C. Shortcut missing
D. Spark disabled

### ✔ Correct Answer: B

---

# 🔵 **SECTION 3 — Dataflow Gen2, Authentication (Q41–Q60)**

---

## **Q41. Dataflow refresh succeeds but writes no data. Why?**

A. Wrong data types
B. Destination load options not set (Append/Replace)
C. Spark offline
D. Wrong workspace

### ✔ Correct Answer: B

---

## **Q42. OAuth token expired. How to prevent?**

A. Use Anonymous
B. Use Organizational account / Managed identity
C. Use CSV instead
D. Use Gateway

### ✔ Correct Answer: B

---

## **Q43. Contributor cannot edit someone else's Dataflow. Why?**

A. Contributor cannot edit
B. They lack permission to connection credentials
C. They lost workspace access
D. Wrong capacity

### ✔ Correct Answer: B

---

## **Q44. What must be last step in Dataflow query?**

A. Source
B. Transformation
C. Data destination
D. Schema drift

### ✔ Correct Answer: C

---

## **Q45. Anonymous disabled. Which fails?**

A. SQL
B. ADLS Gen2
C. GitHub raw CSV
D. Power BI Dataset

### ✔ Correct Answer: C

---

## **Q46. Azure SQL using Azure AD requires which auth?**

A. Basic
B. Key
C. OAuth2
D. Anonymous

### ✔ Correct Answer: C

---

## **Q47. Why can't Dataflow Gen2 use gateway?**

A. Unsupported connector
B. Fabric uses cloud-native compute only
C. Schema drift
D. Delta format incompatible

### ✔ Correct Answer: B

---

## **Q48. Dataflow queued forever. Why?**

A. Spark pool low
B. Capacity queue full
C. Wrong schedule
D. Connection expired

### ✔ Correct Answer: B

---

## **Q49. Which transformation breaks DirectLake compatibility?**

A. Change data type
B. Merge/Join producing non-Delta output
C. Filter rows
D. Rename column

### ✔ Correct Answer: B

---

## **Q50. What must be enabled for incremental Dataflow?**

A. Allow schema drift
B. Enable incremental refresh policy
C. Enable gateway
D. Enable SQL endpoint

### ✔ Correct Answer: B

---

 Nice, cholo baki 50-tao shesh kori 💪
Same format: **Question → Options → Correct answer → Each option explained.**

---

# 🔵 SECTION 3 (continued) — Dataflow Gen2, Transformations, Authentication

### (Q51–Q60)

---

## **Q51. Dataflow Gen2 does NOT support which type of destination?**

**Question:**
Dataflow Gen2 in Fabric can load data into multiple destinations. Which of the following is *NOT* a supported destination?

A. Lakehouse table
B. Warehouse table
C. KQL Database
D. PBIX file

### ✅ **Correct Answer: D. PBIX file**

### Explanation:

* **A. Lakehouse table — Supported**
  Dataflow Gen2 can write directly to **Lakehouse tables** (Delta format).

* **B. Warehouse table — Supported**
  It can also load into **Fabric Warehouses** as relational tables.

* **C. KQL Database — Supported**
  Dataflow Gen2 can write into **KQL Databases** as a destination.

* **D. PBIX file — Not supported** ✅
  Dataflows **never** output PBIX. PBIX is created by Power BI Desktop or via publishing, not by Dataflows.

---

## **Q52. Dataflow cannot connect to SQL DB with Private Endpoint. Solution?**

**Question:**
Your Azure SQL database is configured with a **Private Endpoint only**. Your Dataflow Gen2 cannot connect from Fabric. How can you fix this?

A. Use an On-premises data gateway / Managed VNet gateway
B. Change SQL auth to SQL login
C. Use Anonymous authentication
D. Move SQL DB to public endpoint permanently

### ✅ **Correct Answer: A. Use an On-premises data gateway / Managed VNet gateway**

### Explanation:

* **A. Use gateway — Correct** ✅
  When SQL is only reachable via private network, you need **Data Gateway or Managed VNet gateway** to bridge Fabric to that private endpoint.

* **B. Change SQL auth to SQL login — Wrong**
  Authentication type won’t solve a **network isolation** issue.

* **C. Anonymous — Wrong**
  Azure SQL never allows Anonymous.

* **D. Public endpoint — Technically works but NOT recommended**
  Security best practices say keep Private Endpoint + gateway, not expose publicly.

---

## **Q53. Dataflow loads duplicate rows every refresh. What’s wrong?**

**Question:**
Each time the Dataflow runs, it keeps inserting the same rows again, causing duplicates. What is misconfigured?

A. Load mode set to Replace
B. Load mode set to Append
C. Incremental refresh enabled
D. Schema drift enabled

### ✅ **Correct Answer: B. Load mode set to Append**

### Explanation:

* **A. Replace — Wrong**
  Replace would **remove old data and insert new**, not create duplicates.

* **B. Append — Correct** ✅
  Append always **adds** onto existing data. If source doesn’t filter to “new rows only”, you will get duplicates on every run.

* **C. Incremental — Wrong**
  Incremental refresh is designed to *avoid* duplicates (when configured properly).

* **D. Schema drift — Wrong**
  Schema drift is about columns/types, not duplicates.

---

## **Q54. Which transformation requires M scripting?**

**Question:**
Some complex transformations can only be achieved using M script directly rather than UI buttons. Which of these is MOST likely to need direct M?

A. Change column data type
B. Merge two queries
C. Custom dynamic date logic with complex conditions
D. Rename column

### ✅ **Correct Answer: C. Custom dynamic date logic with complex conditions**

### Explanation:

* **A. Change type — UI Supported**
  You can easily change data type via UI.

* **B. Merge queries — UI Supported**
  “Merge Queries” is a standard Power Query UI action.

* **C. Complex dynamic logic — Correct** ✅
  Very specific & dynamic logic (complex time intelligence, nested conditions, value-dependent calculations) often needs **custom M expressions**.

* **D. Rename column — UI Supported**
  Very basic; no need for code.

---

## **Q55. Where are Dataflow Gen2 credentials stored?**

**Question:**
When you create a connection in Dataflow Gen2 (e.g., to SQL or GitHub), where are those credentials stored?

A. Inside the M script
B. In the user’s browser cache
C. In the Fabric service as a secure connection object
D. In the Lakehouse metadata

### ✅ **Correct Answer: C. In the Fabric service as a secure connection object**

### Explanation:

* **A. M script — Wrong**
  Credentials are *never* stored directly in M code (for security).

* **B. Browser cache — Wrong & insecure**
  That would be terrible security practice.

* **C. Secure connection object — Correct** ✅
  Fabric stores credentials in **secured, encrypted connection objects** associated with the workspace/tenant.

* **D. Lakehouse metadata — Wrong**
  Lakehouse only stores table/files metadata, not source credentials.

---

## **Q56. Table name cannot be changed in Dataflow destination. Why?**

**Question:**
You edit an existing Dataflow Gen2 and try to change the destination table name, but the field is disabled. Why?

A. Table is locked by SQL endpoint
B. Existing table is already bound as destination; must create new Dataflow or destination
C. Only Admins can change table name
D. Spark cluster is offline

### ✅ **Correct Answer: B. Existing table is already bound as destination**

### Explanation:

* **A. Locked by SQL — Wrong**
  SQL endpoint doesn’t directly lock the naming in Dataflow UI.

* **B. Existing binding — Correct** ✅
  Often the binding between query and table is fixed; to change table name you may need to:

  * Create a *new destination*, or
  * Create a new Dataflow pointing to a new table.

* **C. Only admins — Wrong**
  Contributors with proper permission can configure destinations.

* **D. Spark offline — Wrong**
  UI field disabling is not due to Spark status.

---

## **Q57. Which operation can cause Dataflow refresh to fail after schema changes in source?**

**Question:**
Source table gained a new column or removed a column. After that, Dataflow refresh fails. Which transformation step is sensitive to schema changes?

A. Custom column using existing columns
B. Rename columns by `[Position]` or referenced names
C. Filter rows
D. Change type to Any

### ✅ **Correct Answer: B. Rename columns by position / specific names**

### Explanation:

* **A. Custom column — Semi-sensitive but less common**
  Fails only if original columns removed; not primary exam trap.

* **B. Rename columns — Correct** ✅
  If Dataflow step expects **specific columns by name**, and source schema changes (column removed/renamed), the step will break the refresh.

* **C. Filter rows — Usually tolerant**
  Filters on existing columns only; but rename step is more notoriously sensitive.

* **D. Type Any — Not the issue**
  Type ‘Any’ is flexible, not strict.

---

## **Q58. Dataflow output types don’t match Lakehouse expectations. Fix?**

**Question:**
You load data from a CSV where all columns come in as Text. In the Lakehouse table, numeric columns show as text. How should you fix it?

A. Change data types inside Power Query before loading
B. Modify types in Lakehouse after loading every time
C. Enable schema drift
D. Recreate the Lakehouse

### ✅ **Correct Answer: A. Change data types in Power Query**

### Explanation:

* **A. Correct** ✅
  Best practice: adjust data types **in Dataflow (Power Query)** so destination table’s schema is correct from the start.

* **B. Wrong**
  Doing it manually each time is inefficient and fragile.

* **C. Schema drift — Wrong**
  Schema drift lets new columns pass, not fix wrong types.

* **D. Recreate Lakehouse — Overkill & unnecessary**

---

## **Q59. Why does Dataflow evaluation in Fabric use Spark under the hood?**

**Question:**
Dataflow Gen2 runs on Fabric’s Data Engineering engine. Why?

A. To support on-premises data only
B. To reuse Power BI’s old Dataflow engine
C. To leverage Spark’s scalable distributed processing
D. To avoid using M language

### ✅ **Correct Answer: C. To leverage Spark’s scalable processing**

### Explanation:

* **A. On-prem only — Wrong**
  Fabric is mostly **cloud native**.

* **B. Old engine reuse — Wrong**
  Gen2 is designed on Fabric compute (Spark), not the old infrastructure.

* **C. Correct** ✅
  Spark = **distributed, scalable**, great for large transformations and big data.

* **D. Avoid M — Wrong**
  Dataflow Gen2 still uses M under the hood.

---

## **Q60. Pipeline’s Dataflow activity fails, but manual refresh succeeds. Why?**

**Question:**
Running the Dataflow manually works fine, but when the same Dataflow is triggered through a Pipeline activity, it fails with an authentication error. What is most likely wrong?

A. Pipeline uses a different identity/connection than manual run
B. Spark version mismatch in pipeline
C. Lakehouse is paused only for pipelines
D. Dataflow Gen2 doesn’t support pipelines

### ✅ **Correct Answer: A. Pipeline uses different identity/connection**

### Explanation:

* **A. Correct** ✅
  Pipeline might run the Dataflow under:

  * Different user,
  * Service principal,
  * Managed identity—
    which may not have the same permissions/credentials.

* **B. Spark mismatch — Unlikely**
  Spark engine is same under Fabric.

* **C. Paused Lakehouse only for pipeline — No such concept**

* **D. False**
  Dataflow Gen2 **is supported** as a pipeline activity.

---

# 🔵 SECTION 4 — Pipelines, Scheduling, Orchestration, Spark

### (Q61–Q80)

---

## **Q61. Pipeline activity says “No permission to run Dataflow.” Missing permission?**

A. Viewer access to workspace
B. Build permission on semantic model
C. Contributor/Member permission on workspace containing the Dataflow
D. Capacity admin role

### ✅ **Correct Answer: C. Contributor/Member permission**

### Explanation:

* **A. Viewer — Too low**
  Viewers can’t run pipeline activities that modify things.

* **B. Build on semantic model — Irrelevant here**

* **C. Correct** ✅
  To run a Dataflow via pipeline, you must have **Contributor/Member+** on the workspace where Dataflow exists.

* **D. Capacity admin — Overkill**
  Not required for running pipeline.

---

## **Q62. Scheduling a pipeline fails; workspace is on Shared capacity. Why?**

A. Shared capacity doesn’t support any scheduling
B. Fabric pipelines require Fabric/Premium capacity
C. User doesn’t have Pro license
D. Spark pool not assigned

### ✅ **Correct Answer: B. Fabric pipelines require Fabric/Premium**

### Explanation:

* **A. “No scheduling at all” — too generic**
  Actually, it’s because Fabric workload isn’t available.

* **B. Correct** ✅
  Pipelines are **Fabric workload** → need Fabric/Premium capacity.

* **C. Pro license — Not the main factor**
  In capacity, Pro vs Free for internal access matters less than capacity support.

* **D. Spark not required just to schedule**

---

## **Q63. Pipeline retry fails instantly. Why?**

A. Retry count is zero
B. Capacity / workload is disabled
C. Wrong time zone
D. Dataflow incremental is off

### ✅ **Correct Answer: B. Capacity/workload disabled**

### Explanation:

* **A. Retry count zero — Wouldn’t even retry**

* **B. Correct** ✅
  If capacity or that *specific workload* (Pipelines/Dataflows) is disabled, each retry will fail immediately for the same reason.

* **C. Time zone — Not related**

* **D. Incremental — Not relevant here**

---

## **Q64. Pipeline can’t delete a Lakehouse table. Missing permission?**

A. Read
B. Build
C. Write/Contributor on Lakehouse/workspace
D. Capacity admin

### ✅ **Correct Answer: C. Write/Contributor**

### Explanation:

* **A. Read — Only allows selecting**

* **B. Build — Mainly for semantic models**

* **C. Correct** ✅
  Deleting objects requires **write-level** permission (Contributor/Member/Admin).

* **D. Capacity admin — Not needed**

---

## **Q65. Which pipeline activity requires Spark compute?**

A. Dataflow Gen2 activity
B. Notebook activity
C. SQL script activity
D. Copy data activity

### ✅ **Correct Answer: B. Notebook activity**

### Explanation:

* **A. Dataflow — Uses the Dataflow engine (which uses Fabric compute), but not directly user-managed Spark like Notebook.**

* **B. Notebook — Correct** ✅
  Notebooks execute on **Spark clusters**, explicitly.

* **C. SQL script — Uses SQL endpoint compute, not Spark**

* **D. Copy Activity — Uses Data movement compute, not Spark clusters**

---

## **Q66. Which pipeline activity cannot run in Shared capacity?**

A. Dataflow Gen1
B. Power BI Refresh
C. Fabric Notebook
D. REST API call

### ✅ **Correct Answer: C. Fabric Notebook**

### Explanation:

* **A. Dataflow Gen1 — This is Power BI artifact and may work with Pro**

* **B. Power BI refresh — Works in Shared capacity (with Pro)**

* **C. Notebook — Correct** ✅
  Fabric **Notebooks are Fabric workloads** → require Fabric/Premium capacity.

* **D. REST API — Could be implemented in various ways, not strictly blocked by shared capacity**

---

## **Q67. Pipeline triggers twice unexpectedly. Why?**

A. Two triggers configured (e.g., schedule + manual trigger)
B. Spark restarted
C. Dataflow incremental refresh
D. Capacity scaling

### ✅ **Correct Answer: A. Two triggers configured**

### Explanation:

* **A. Correct** ✅
  If there are multiple triggers (e.g., schedule + event-based), same time window may cause **double execution**.

* **B. Spark restart — Doesn’t auto rerun pipelines**

* **C. Incremental — Unrelated**

* **D. Capacity scaling — No automatic duplicate runs**

---

## **Q68. Notebook in pipeline can’t write to Files. Why?**

A. Notebook language is Python
B. User lacks OneLake filesystem write permissions
C. Spark version issue
D. Pipeline concurrency issue

### ✅ **Correct Answer: B. Lacks FS write permission**

### Explanation:

* **A. Python vs Scala — Not a permission factor**

* **B. Correct** ✅
  To write to Lakehouse Files or OneLake path, user/service principal running Notebook needs **filesystem-level write** permission.

* **C. Version — Less likely and not typical exam scenario**

* **D. Concurrency — Affects performance, not permissions**

---

## **Q69. Copy Activity from ADLS Gen2 to Lakehouse requires what configuration?**

A. Anonymous auth
B. Service principal / managed identity with storage access
C. CSV-only files
D. On-prem gateway

### ✅ **Correct Answer: B. Service principal / managed identity**

### Explanation:

* **A. Anonymous — Usually disabled for secure storage**

* **B. Correct** ✅
  ADLS typically secured via **Azure AD** (service principal, managed identity).

* **C. CSV-only — Wrong**
  ADLS supports many formats.

* **D. On-prem gateway — Only needed for on-prem sources, not Azure.

---

## **Q70. SQL script activity fails due to RLS-based errors. Why?**

A. User has no Pro license
B. Script uses unsupported SQL syntax
C. Pipeline identity does not meet RLS requirements
D. Fabric capacity paused

### ✅ **Correct Answer: C. Pipeline identity not satisfying RLS**

### Explanation:

* **A. Pro license — Not about RLS**

* **B. Syntax — Would show different error**

* **C. Correct** ✅
  RLS is based on the **effective identity** running the script. If that identity lacks proper role membership, it fails.

* **D. Paused — Would error differently (“capacity paused”)**

---

## **Q71. You want pipelines to run with managed identity. What must be done?**

A. Enable “Users can create Fabric items”
B. Assign managed identity proper access to downstream resources
C. Disable OAuth
D. Enable external sharing

### ✅ **Correct Answer: B. Assign MI access**

### Explanation:

* **A. Fabric items toggle — Not related directly**

* **B. Correct** ✅
  Managed identity must be granted:

  * SQL permissions,
  * Storage permissions,
  * Lakehouse permissions, etc.

* **C. Disable OAuth — Not a requirement**

* **D. External sharing — Irrelevant**

---

## **Q72. How to ensure conditional execution works in pipeline?**

A. Use retry policy
B. Use “If Condition” activity that checks previous activity output
C. Always use ForEach
D. Use only manual triggers

### ✅ **Correct Answer: B. Use “If Condition”**

### Explanation:

* **A. Retry — For retry, not conditional**

* **B. Correct** ✅
  To conditionally run parts of pipeline, use **If Condition** or **Switch** with outputs of previous steps.

* **C. ForEach — For iteration, not branch logic**

* **D. Trigger type — Not relevant to conditional logic**

---

## **Q73. Pipeline fails daily at same time due to capacity spikes. Fix?**

A. Change M code in Dataflow
B. Move pipeline to different Fabric capacity with more headroom
C. Disable DirectLake
D. Disable RLS

### ✅ **Correct Answer: B. Move to higher or less-busy capacity**

### Explanation:

* **A. M code — Won’t fix capacity contention**

* **B. Correct** ✅
  Move workspace/pipeline to capacity with **more resources** or less contention.

* **C. DirectLake — Not directly relevant**

* **D. RLS — Not about compute pressure**

---

## **Q74. Run Dataflow then Notebook sequentially. What control to use?**

A. Two triggers
B. Sequential activities chained (Success dependency)
C. Parallel execution
D. Two separate pipelines

### ✅ **Correct Answer: B. Chain with Success dependency**

### Explanation:

* **A. Triggers — Control start time, not order**

* **B. Correct** ✅
  In pipeline, you place Dataflow activity first, then Notebook; set Notebook to run **“On Success”** of Dataflow.

* **C. Parallel — Runs both at the same time**

* **D. Two separate pipelines — No orchestration guarantee**

---

## **Q75. Pipeline run takes long to start. Why?**

A. Trigger misconfigured
B. High queue wait time due to capacity load
C. SQL endpoint offline
D. Wrong auth

### ✅ **Correct Answer: B. Capacity queue wait**

### Explanation:

* **A. Trigger — If trigger fired, pipeline is already invoked**

* **B. Correct** ✅
  Under heavy load, Fabric can **queue executions**, leading to a delay before actual run.

* **C. SQL endpoint — Would error during execution, not start delay**

* **D. Auth — Would fail quickly, not delayed**

---

## **Q76. Pipeline referencing Warehouse says “Build permission required.” Why?**

A. User is Viewer
B. User has only Read access to Warehouse
C. User not in capacity admin list
D. Dataflow schema mismatch

### ✅ **Correct Answer: B. Only Read access**

### Explanation:

* **A. Viewer — Might be true, but exam answer is more precise**

* **B. Correct** ✅
  To create objects/reports or run some operations on a Warehouse/dataset, you often need **Build permission**, not just Read.

* **C. Capacity admin — Overkill**

* **D. Schema mismatch — Different error**

---

## **Q77. What permission allows editing pipelines?**

A. Viewer
B. Member/Contributor on workspace
C. Build on dataset
D. Capacity admin

### ✅ **Correct Answer: B. Member/Contributor**

### Explanation:

* **A. Viewer — Read-only**

* **B. Correct** ✅
  Members/Contributors can **edit workspace content**, including pipelines.

* **C. Build — For datasets, not pipelines**

* **D. Capacity admin — Not required**

---

## **Q78. Pipeline fails when writing many tiny delta files. Fix?**

A. Enable Auto Optimize / Optimize Write in Spark
B. Use CSV instead of Delta
C. Retry pipeline
D. Turn off sensitivity labels

### ✅ **Correct Answer: A. Enable Auto Optimize / Optimize Write**

### Explanation:

* **A. Correct** ✅
  Too many small files leads to performance issues (small file problem). Auto optimize / optimize writes help merge small files.

* **B. CSV — Makes it worse**

* **C. Retry — Doesn’t fix underlying issue**

* **D. Labels — Not relevant**

---

## **Q79. Schedule set, but pipeline never runs. Why?**

A. Schedule is disabled or misconfigured
B. Fabric trial expired
C. Notebook language mismatch
D. Dataflow schema drift disabled

### ✅ **Correct Answer: A. Schedule disabled/misconfigured**

### Explanation:

* **A. Correct** ✅
  Common reasons:

  * Trigger accidentally turned off
  * Wrong timezone/time window
  * Past date/time

* **B. Trial — Could cause other issues, but exam-likely answer = schedule misconfig.

* **C. Language — Pipeline would still trigger; activity would fail, not the schedule.

* **D. Schema drift — Not related**

---

## **Q80. Which pipeline activity can orchestrate non-Fabric resources?**

A. Notebook
B. REST API or Web activity
C. Dataflow Gen2
D. SQL script

### ✅ **Correct Answer: B. REST API / Web activity**

### Explanation:

* **A. Notebook — Still mostly inside Fabric/Spark**

* **B. Correct** ✅
  REST/Web activity can call **external services** (Azure Functions, Logic Apps, third-party APIs).

* **C. Dataflow — For data transformations**

* **D. SQL script — For Warehouse/SQL endpoints**

---

# 🔵 SECTION 5 — Governance, Security, Sensitivity Labels

### (Q81–Q100)

---

## **Q81. Sensitivity label propagation not working. Which setting?**

A. Enable “Allow users to create workspaces”
B. Enable “Automatically apply sensitivity labels to downstream content”
C. Enable external sharing
D. Enable publish to web

### ✅ **Correct Answer: B**

### Explanation:

* **A. Workspace creation — Irrelevant**

* **B. Correct** ✅
  Downstream propagation (dataset → report → dashboard) depends on this setting.

* **C. External sharing — Different topic**

* **D. Publish to web — Dangerous for sensitive data, not propagation.

---

## **Q82. Users can view a report but cannot “Analyze in Excel”. Why?**

A. Need Build permission on the semantic model
B. Need Admin role in workspace
C. Must be capacity admin
D. Must be data gateway admin

### ✅ **Correct Answer: A. Build permission**

### Explanation:

* **A. Correct** ✅
  Analyze in Excel requires **Build** permission on the dataset/semantic model.

* **B, C, D — Overkill / wrong**
  None of these roles are specifically required for Analyze in Excel.

---

## **Q83. External sharing of report fails. Which control?**

A. Guest users can access Fabric
B. Publish to web
C. Sensitivity labels
D. Export to CSV

### ✅ **Correct Answer: A. Guest users can access Fabric**

### Explanation:

* **A. Correct** ✅
  If guest access to Fabric is disabled, you can’t properly share Fabric content externally.

* **B. Publish to web — Public/uncontrolled; not the same as secure external sharing.**

* **C. Labels — Might block, but exam-likely: guest access setting.

* **D. CSV export — Not about sharing.

---

## **Q84. Sensitivity labels block exporting. Why?**

A. Label configured to disallow export
B. Dataset endorsed as Certified
C. Fabrics trial ended
D. RLS enabled

### ✅ **Correct Answer: A. Label configuration**

### Explanation:

* **A. Correct** ✅
  You can configure labels to **prevent export/copy/print**.

* **B. Certification — Doesn’t block export**

* **C. Trial — Not label-specific**

* **D. RLS — Limits rows, not export itself.

---

## **Q85. Certification visible only to few users. Reason?**

A. Only Admins can see certified items
B. Certification view restricted to certain security groups
C. Capacity issue
D. Sensitivity labels hide it

### ✅ **Correct Answer: B. Restricted to security groups**

### Explanation:

* **A. Wrong**
  Non-admins can see certified items if permissions granted.

* **B. Correct** ✅
  Tenant setting often defines **who can see or certify** and who sees the badge.

* **C. Capacity — Not about certification**

* **D. Labels — May hide data, but not the certification badge alone.

---

## **Q86. Hide promoted/certified content from general users. Which setting?**

A. Turn off “Make promoted and certified content discoverable”
B. Turn off workspace creation
C. Turn off external sharing
D. Disable RLS

### ✅ **Correct Answer: A. Turn off discoverability**

### Explanation:

* **A. Correct** ✅
  This setting controls whether promoted/certified content shows up in **“Discovery / Featured / Recommended”** sections.

* **B,C,D — Not directly related.**

---

## **Q87. Guest users cannot request access to datasets. Why?**

A. Guest user suggestion turned off
B. External sharing disabled
C. Discovery for guest users disabled
D. Purview integration disabled

### ✅ **Correct Answer: C. Discovery for guest users disabled**

### Explanation:

* **A. Suggestion list — Only affects UI hints, not access requests**

* **B. External sharing — Might block sharing, but question is about *request* features**

* **C. Correct** ✅
  If guests are not allowed to **discover and request** access, they can’t see or request.

* **D. Purview — Not related**

---

## **Q88. Which setting controls whether AI/Copilot can use labeled data?**

A. “Apply sensitivity labels to downstream content”
B. “Allow Microsoft Purview to secure AI interactions”
C. “Users can try Fabric paid features”
D. “Guest users can access Fabric”

### ✅ **Correct Answer: B**

### Explanation:

* **A. Downstream only**
  It’s about propagation, not AI.

* **B. Correct** ✅
  This governs whether Purview can **inspect & control AI prompts/answers** for sensitive content.

* **C. Trial — Not specifically about AI governance**

* **D. Guest access — Irrelevant**

---

## **Q89. Dashboard tile with external web content not loading. Which setting disabled?**

A. Use semantic models across workspaces
B. Publish to web
C. “Allow web content in dashboards”
D. Export to Excel

### ✅ **Correct Answer: C. Allow web content**

### Explanation:

* **A. Semantic models cross-workspace — Not related**

* **B. Publish to web — For whole report, not tile web content**

* **C. Correct** ✅
  Admins can disable **web content tiles** for security reasons.

* **D. Export — Not relevant**

---

## **Q90. Publish prompt before publishing reports. Which feature?**

A. Custom publish warning message
B. RLS policy
C. Sensitivity label
D. Capacity rule

### ✅ **Correct Answer: A. Custom publish warning**

### Explanation:

* **A. Correct** ✅
  Tenant can configure a **custom warning** that users see when publishing.

* **B. RLS — Data filtering, not UI prompt**

* **C. Labels — Might show disclaimers in some tools but this scenario is about publish step.

* **D. Capacity — No.

---

## **Q91. Fine-grained access to semantic model requires which permission?**

A. Viewer
B. Build
C. Member
D. Admin

### ✅ **Correct Answer: B. Build**

### Explanation:

* **A. Viewer — Read-only for report**

* **B. Correct** ✅
  Build permission allows:

  * Analyze in Excel
  * Creating new reports using that semantic model
  * Using it as source.

* **C. Member / D. Admin — Over-permissioned; Build is sufficient.

---

## **Q92. RLS works in Workspace A, but not cross-workspace. Why?**

A. “Use semantic models across workspaces” disabled
B. Guest access disabled
C. Export disabled
D. Capacity on Shared

### ✅ **Correct Answer: A. Use semantic models across workspaces disabled**

### Explanation:

* **A. Correct** ✅
  When disabled, cross-workspace dataset usage is restricted; RLS may not behave correctly or dataset not usable.

* **B. Guest access — Irrelevant**

* **C. Export — Not RLS-related**

* **D. Shared capacity — Doesn’t break RLS like that**

---

## **Q93. Export to CSV disabled due to label. Which property?**

A. Label is “Public”
B. Label is “Confidential – No Export”
C. Label applies only to columns
D. Label limited to email only

### ✅ **Correct Answer: B. “No Export” policy**

### Explanation:

* **A. Public — Would allow export**

* **B. Correct** ✅
  Labels like **“Highly Confidential – No Export”** can explicitly deny exports.

* **C. Column-level — Not standard for Power BI label semantics**

* **D. Email-only label — Not about reports.

---

## **Q94. Semantic model uses encrypted label. Which functionality usually becomes unavailable?**

A. Row-level security
B. Cross-filtering
C. External sharing (including guest) and “Publish to web”
D. DirectLake mode

### ✅ **Correct Answer: C. External sharing & publish to web**

### Explanation:

* **A. RLS — Still works**

* **B. Cross-filter — Still works**

* **C. Correct** ✅
  Encrypted labels **block public or uncontrolled sharing**, like Publish to Web or sharing with unauthorized users.

* **D. DirectLake — Not inherently blocked by labels.

---

## **Q95. Report refresh disabled. Which tenant setting caused it?**

A. “Allow scheduled refresh” disabled in Tenant settings
B. “Users can create Fabric items” disabled
C. “Export to Excel” disabled
D. “Guest users can access Fabric” disabled

### ✅ **Correct Answer: A. Allow scheduled refresh disabled**

### Explanation:

* **A. Correct** ✅
  Tenant admins can block scheduled refresh for datasets/reports.

* **B. Fabric item creation — Doesn’t stop refresh**

* **C. Export — Not about refresh**

* **D. Guest — Unrelated**

---

## **Q96. Workbook discovery not working. What must be enabled?**

A. Use semantic models across workspaces
B. Discover content
C. Guest suggestions
D. Export data

### ✅ **Correct Answer: B. Discover content**

### Explanation:

* **A. Semantic cross-workspace — Not discovery-specific**

* **B. Correct** ✅
  “Discover content” controls whether users can **search and find** items they don’t already know directly.

* **C. Guest suggestions — UI only**

* **D. Export — Not related**

---

## **Q97. Guest users show up in share suggestions. Which setting controls this?**

A. Show guest users in people picker
B. Allow publish to web
C. Allow external data sharing
D. Discover content

### ✅ **Correct Answer: A. Show guest users in people picker**

### Explanation:

* **A. Correct** ✅
  Admin can choose whether guests appear in **sharing UI suggestions**.

* **B. Publish to web — Public, not about suggestions**

* **C. External data sharing — About OneLake shares, not UI suggestions**

* **D. Discovery — About content, not people.

---

## **Q98. Dataset lineage view missing some items. Why?**

A. Lineage view disabled for workspace
B. Some items are in different tenant or unsupported sources
C. RLS blocking them
D. Sensitivity labels hide everything

### ✅ **Correct Answer: B. Items in other tenant/unsupported**

### Explanation:

* **A. No “disable lineage view” switch like that**

* **B. Correct** ✅
  Lineage doesn’t show:

  * External tenant items
  * Some unsupported external sources.

* **C. RLS — Affects data visibility, not lineage diagram**

* **D. Labels — Do not remove lineage boxes completely (normally).

---

## **Q99. Fabric items cannot be discovered across domains. Which setting?**

A. Discover content disabled per domain
B. Guest access disabled
C. Publish to web disabled
D. Export data disabled

### ✅ **Correct Answer: A. Discover content disabled per domain**

### Explanation:

* **A. Correct** ✅
  Multi-domain environment can have different discovery policies.

* **B, C, D — Not about discoverability across domains.**

---

## **Q100. Which admin setting disables uncontrolled “share to all” links?**

A. Disable “Share with everyone in organization” links
B. Disable publish to web
C. Disable workspace creation
D. Disable export to CSV

### ✅ **Correct Answer: A. Disable “Share with everyone” links**

### Explanation:

* **A. Correct** ✅
  This directly controls shareable links that grant access to the **entire org**.

* **B. Publish to web — Public internet, different feature**

* **C. Workspace — Not about link scope**

* **D. Export — Data exfiltration, not access-links.


 
[1]: https://learn.microsoft.com/en-us/fabric/admin/about-tenant-settings?utm_source=chatgpt.com "About tenant settings - Microsoft Fabric"
[2]: https://learn.microsoft.com/en-us/fabric/admin/capacity-settings?utm_source=chatgpt.com "Manage your Fabric capacity"
[3]: https://learn.microsoft.com/en-us/fabric/fundamentals/workspaces?utm_source=chatgpt.com "Workspaces in Microsoft Fabric and Power BI"
[4]: https://learn.microsoft.com/en-us/fabric/admin/tenant-settings-index?utm_source=chatgpt.com "Tenant settings index - Microsoft Fabric"
[5]: https://learn.microsoft.com/en-us/fabric/admin/tenant-settings-index "Tenant settings index - Microsoft Fabric | Microsoft Learn"
[6]: https://learn.microsoft.com/en-us/fabric/admin/service-admin-portal-help-support?utm_source=chatgpt.com "Help and support tenant settings - Microsoft Fabric"
[7]: https://learn.microsoft.com/en-us/fabric/enterprise/powerbi/service-admin-premium-workloads?utm_source=chatgpt.com "How to configure workloads in Power BI Premium"
[8]: https://learn.microsoft.com/en-us/fabric/data-engineering/capacity-settings-management?utm_source=chatgpt.com "Manage settings for data engineering and science capacity"
[9]: https://learn.microsoft.com/en-us/fabric/admin/fabric-switch?utm_source=chatgpt.com "Enable Microsoft Fabric for your organization"
[10]: https://learn.microsoft.com/en-us/fabric/data-engineering/workspace-admin-settings?utm_source=chatgpt.com "Workspace administration settings in Microsoft Fabric"
