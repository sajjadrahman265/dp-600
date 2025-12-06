Nice, eita ekdom “admin level boss mode” topic 😄
Cholo eta ke **bora chhobi → then group by group** bujhi, jate DP-600 question askle tumi confident thako.

---

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

Just bolo:

> “Admin setting–based DP-600 questions dao”
> ar ami straight সেই direction-e question + answer + reasoning diye debo.

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
