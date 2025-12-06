Thik ache, ekhon amra “boss level shortcut” + “exam boxing practice” duti ek sathe korbo 😄

I’ll do it in 2 parts:

1. **Key rules & patterns to memorize** (very short, high-impact)
2. **Rapid-fire revision – Round 1 (10 questions)**

---

## 🧠 Part 1 – Key Rules & Patterns To Memorize

### 1️⃣ Tenant vs Capacity vs Workspace – ALWAYS think level first

**Tenant level (global):**

* “Users can create Fabric items”
* “Users can try Fabric paid features (trial)”
* Sensitivity labels & export policies
* External/guest access & discovery
* Publish to web
* Discover/promoted/certified content
  👉 If question = “ORG-wide policy / all users / for whole tenant” → **Tenant settings**.

**Capacity level (per F64/F128…):**

* Whether Fabric workloads are enabled (Pipelines/Dataflows/Notebooks)
* Spark limits, concurrency, memory
* Capacity paused or not
  👉 If question = “Insufficient capacity, queued, Spark can’t allocate, Fabric paused” → **Capacity settings**.

**Workspace level:**

* Which capacity it uses (Shared vs Fabric)
* Who is Admin / Member / Contributor / Viewer
* Default Spark pool
  👉 If question = “This workspace can’t create Fabric items / pipelines / Lakehouse” → first check **capacity = Shared?**

---

### 2️⃣ Fabric vs non-Fabric – capacity shortcut

* **Shared capacity**

  * ✅ Reports, dashboards, semantic models
  * ❌ **No** Lakehouse, Warehouse, Dataflow Gen2, Pipelines, Notebook, DirectLake

* **Fabric / Premium capacity**

  * ✅ All of the above **plus** Lakehouse, Warehouse, Dataflow Gen2, Pipeline, Notebook, DirectLake

👉 If question says: “Option not visible / can’t create Lakehouse / Dataflow / Notebook / DirectLake not available” →
Check **Shared vs Fabric** OR **Tenant’s ‘Users can create Fabric items’**.

---

### 3️⃣ Permissions quick map

* **Viewer** → can only see content, no edit/run that changes data.
* **Member / Contributor** → can create & edit workspace items (Dataflow, Pipeline, Lakehouse, Report).
* **Admin** → everything + workspace settings.
* **Build (on semantic model)** →

  * Analyze in Excel
  * Create new reports from that model
  * Use model in other workspaces

👉 If question = “I can see report but can’t Analyze in Excel / can’t build new reports” → **Build permission missing**.

---

### 4️⃣ Dataflow Gen2 – 4 golden rules

1. **Refresh succeeded but table empty?**
   → You forgot **destination (Append/Replace)**.

2. **Duplicates every refresh?**
   → Load mode = **Append** but source not filtered to new rows.

3. **Cannot edit Dataflow someone else made?**
   → You lack permission to **credentials/connection**.

4. **Queued in Pending for a long time?**
   → **Capacity queue full / workload disabled**.

Plus:

* GitHub public CSV → needs **Anonymous** → blocked if tenant disables public/anonymous sources.
* Private Endpoint SQL → needs **gateway / Managed VNet gateway**.

---

### 5️⃣ DirectLake – 3 lines only

* Only under **Fabric/Premium capacity**.
* Works with **Delta tables in OneLake (Lakehouse/Warehouse)**.
* If suddenly slow → **capacity under pressure (cache eviction)**.

---

### 6️⃣ Lakehouse vs Files vs SQL endpoint

* **Tables** = Delta tables, queried via **SQL endpoint**.
* **Files** = OneLake filesystem; needs **filesystem permission** to browse/write.
* You can have permission to query table but **not** view Files.

👉 If question = “Can query table but cannot open Files” → missing **OneLake FS permission**.

Shortcut:

* **Shortcut** = pointer, **NO sync**. If external is outdated or blocked → shortcut shows problem.

---

### 7️⃣ Sensitivity labels & export

* If export/Analyze in Excel blocked and sensitivity mentioned →
  Probably **label has ‘No Export’ policy**.
* Label propagation → needs **“Automatically apply sensitivity labels to downstream content”**.
* AI/Copilot + labels → **“Allow Purview to secure AI interactions”**.

---

### 8️⃣ Guest / External access

* Invited but can’t see anything?
  → **“Guest users can access Fabric”** must be ON.
* Can’t share outside?
  → External sharing / guest / external data share must be ON.
* Appear in people picker?
  → **Show guest users in suggestions**.

---

### 9️⃣ Export / Download vs View-only

* View but no export → change **Export data / Export to Excel / Download report** settings.
* Block PBIX download → **Disable “Download report”**.
* Full public URL (no login) → **Publish to web** (often disabled in secure orgs).

---

### 🔟 Repeated exam traps

* “Users can create Fabric items” = MOST COMMON toggle in tenant and capacity-level questions.
* “Use semantic models across workspaces” → cross-workspace dataset usage + RLS issues.
* Pipeline / Notebook / DirectLake not working? Always ask:

  1. **Capacity?** 2) **Workload enabled?** 3) **Permissions?**

---

## ⚡ Part 2 – Rapid-Fire Revision (Round 1: 10 Questions)

Format:
I’ll ask 10 quick questions.
You reply like:
`Q1-B, Q2-C, ...`

Then I’ll mark correct/wrong + explain very quickly, and we do next round.

---

### 🔥 Round 1 (Admin + Capacity + Fabric basics)

**Q1.** Users can create reports in a workspace but cannot create Lakehouse or Dataflow Gen2.
Which setting is the MOST likely cause?

A. Workspace is in Shared capacity
B. “Users can create Fabric items” disabled
C. Sensitivity labels enabled
D. Export data disabled

---

**Q2.** DirectLake mode is missing for a semantic model. What’s the most likely cause?

A. Too many rows
B. Workspace is in Shared capacity
C. Incremental refresh is off
D. RLS enabled

---

**Q3.** Guest users were invited but see no Fabric items at all.
Which admin toggle is responsible?

A. External data sharing disabled
B. “Guest users can access Fabric” disabled
C. “Users can try Fabric paid features” disabled
D. Discover content disabled

---

**Q4.** Dataflow refresh succeeded but the Lakehouse table still has 0 rows.
What did you forget?

A. Incremental refresh
B. Data destination (Append/Replace)
C. Schema drift
D. Spark cluster

---

**Q5.** A user can query Lakehouse tables via SQL but cannot open the Files folder.
What permission are they missing?

A. Read on Warehouse
B. OneLake filesystem permission
C. Build permission
D. Capacity admin

---

**Q6.** A Dataflow Gen2 connecting to GitHub raw CSV fails. The error says “Anonymous access not allowed.”
Which setting must admin change?

A. Enable public/anonymous data sources
B. Enable Purview
C. Enable DirectLake
D. Enable export

---

**Q7.** A report consumer can view reports but cannot Analyze in Excel.
What permission is missing?

A. Viewer
B. Build
C. Capacity admin
D. Workspace admin

---

**Q8.** A pipeline referencing a Warehouse throws “Build permission required.”
What does the user have right now?

A. Only Read access
B. Only Admin access
C. Only Viewer access
D. Only capacity admin

---

**Q9.** After enabling sensitivity labels, exports (like CSV) are blocked for a specific report.
What is the cause?

A. Label policy is “No Export”
B. Workspace on Shared capacity
C. Dataset not certified
D. RLS enabled

---

**Q10.** You want to stop users from creating any new workspaces in the tenant.
Which setting must you change?

A. Create workspaces (Tenant → Workspace settings)
B. Users can create Fabric items
C. External sharing
D. Export data

---

👉 Now your turn:

Reply with your answers like this:
**`Q1-?, Q2-?, Q3-? ... Q10-?`**

Then I’ll check them, correct where needed, and we’ll do **Round 2** with slightly trickier questions.
