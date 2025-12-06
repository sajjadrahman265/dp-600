Absolutely — **you need a single, clean, structured, flow-based DP-600 Admin + Fabric note**
➡️ Easy to learn
➡️ Easy to revise
➡️ Easy to recall in exam
➡️ Covers all 100-question logic but without the clutter

I will give you **THE definitive study note** → ultra-organized, layered, flowchart-style thinking, memory patterns, exam traps, everything.

---

# ✅ **DP-600 FABRIC ADMIN SUPER NOTES (Organized, Structured, Flow-Based)**

### *(This is your revision-ready “cheat sheet”. Keep this as your master note.)*

---

# 0️⃣ **Three Admin Layers — The ROOT of all DP-600 questions**

Everything in Fabric admin falls into **3 layers**.
If you remember this structure → 60% of admin questions become easy.

```
TENANT → applies to entire organization
CAPACITY → applies to compute resources (F64, F128…)
WORKSPACE → applies to specific teams/projects
```

### ✔ Why important?

Most exam questions ask:

> “Which setting must be changed?”
> → Identify **which layer** the problem is in.

---

# 1️⃣ **TENANT SETTINGS — Organization-wide rules**

*(Most exam traps come from here)*

Think of Tenant as: **What the ORG allows users to do**.

---

## 🔵 1.1 Fabric Enablement Block (TOP 1 most tested)

### 🔥 **MASTER RULE:**

If user cannot see or create *any* Fabric items:

➡️ Always check these 2 first:

```
Tenant Setting: “Users can create Fabric items”
Capacity Setting: Delegate tenant settings (Fabric disabled for specific capacities)
```

### What it controls:

* Lakehouse creation
* Dataflow Gen2 creation
* Warehouse creation
* Pipeline creation
* Notebook creation
* KQL DB creation

### 🔑 Pattern:

**Reports work → Fabric items missing → This setting is OFF.**

---

## 🔵 1.2 Trial, Help, and App Policies

### **Users can try Fabric paid features**

* Allows starting **Fabric trial**.
* OFF = no user can start trial.

### **Custom publish warning**

* Adds a warning message before publishing reports.

### **Users can create apps / org apps**

* Controls new “Organization apps” visibility.

➡️ Exam trap:
*If user cannot see “Org apps” option → this setting is OFF.*

---

## 🔵 1.3 Workspace Governance

Controls WHO can create workspaces and how they behave.

### Key settings:

```
Create workspaces (Everyone / Restricted)
Use semantic models across workspaces
Personal workspace assignment block
Workspace retention period
Auto-convert PBIX → PBIR
```

### Most important exam patterns:

### ✔ If cross-workspace report creation fails →

**“Use semantic models across workspaces” is OFF.**

### ✔ If workspace creation must be restricted →

**“Create workspaces” → Only specific security groups.**

---

## 🔵 1.4 Sensitivity Labels & Purview (HIGH exam weight)

This entire block controls:

* Label visibility
* Label inheritance
* Label propagation
* Blocking export/print/share
* AI + Copilot governance

### Key toggles:

```
Allow users to apply sensitivity labels
Automatically apply labels to downstream content
Allow Purview to secure AI interactions
Restrict labeled content from being shared org-wide
```

### Exam traps:

✔ If export blocked unexpectedly →
**Label = "No Export"** or **Downstream label propagation**.

✔ If Copilot blocked →
**Purview AI security OFF**.

✔ If labels not visible →
**"Allow sensitivity labels" = OFF**.

---

## 🔵 1.5 Export & Sharing (Most exam trick questions)

### These settings control:

* Export to Excel/CSV
* Download PBIX
* Publish to web
* External data sharing
* Guest access
* Share-to-org links

### KEY RULES:

#### 🔥 1. **Block download PBIX?**

→ Disable **“Download report”**

#### 🔥 2. **Block export but allow viewing?**

→ Disable **“Export data / Export Excel / Export CSV”**

#### 🔥 3. **External users cannot access?**

Check sequence:

```
Guest users can access Fabric → ON
Users can invite guest users → optional
External data sharing → ON (for OneLake)
Publish to web → OFF (if secure org)
```

#### 🔥 4. **Discover content?**

→ Controls whether users can find content through search/discovery.

---

## 🔵 1.6 Integration Settings

(Recall using a simple rule)

```
If something integrates with Excel / XMLA / SharePoint / Maps / External DB → 
It is under Tenant’s Integration settings.
```

Examples:

* XMLA read/write
* Analyze in Excel
* SharePoint integration
* SSO for external sources
* Custom visuals controls

---

# 2️⃣ **CAPACITY SETTINGS — The Engine Room**

*(Every compute problem originates here)*

Fabric capacity is what makes:

* Spark run
* Dataflow Gen2 run
* Pipelines run
* DirectLake cache run
* SQL Endpoint run

---

## 🔵 Capacity = **Your Fabric Compute Brain**

### Main controls:

```
Capacity admins
Workload enable/disable (Pipelines / Dataflows / Spark)
Memory and concurrency limits
Pause / Resume capacity
Delegate tenant settings
```

---

### ⭐ STAR RULES (Most exam tested) ⭐

### ✔ If Notebook fails →

**Spark workload disabled** OR **capacity overloaded**.

### ✔ If Pipeline fails →

**Pipelines workload disabled**.

### ✔ If DirectLake slow →

**Capacity pressure → cache eviction** → acts like DirectQuery.

### ✔ If Dataflow queued forever →

**Capacity queue full**.

### ✔ If workspace moved to capacity but still cannot use Fabric →

**Delegate tenant settings override tenant setting**.

---

# 3️⃣ **WORKSPACE SETTINGS — Team-level configuration**

These are more straightforward.

### Workspace controls:

```
Capacity assignment (Shared vs Fabric)
Default Spark pool
Workspace admins / members / contributors / viewers
Connections
Data engineering / SQL settings
```

---

### ⭐ KEY RULE:

If workspace is in → **Shared capacity**
Users CAN'T do:

* Lakehouse
* Dataflow Gen2
* Notebook
* Pipeline
* Warehouse
* DirectLake

➡️ Only Power BI features allowed.

---

# 4️⃣ **LAKEHOUSE & DELTA — Core Concepts Flow**

Fabric Lakehouse uses:

```
Files → raw storage
Tables → Delta format
SQL Endpoint → query interface
```

### Memory Patterns:

### ✔ Files ≠ Tables

Files must be **registered as tables**.

### ✔ Delta tables version automatically

Any write → creates new version.

### ✔ Shortcuts

= Live pointer → NO sync.

### ✔ Permissions

SQL tables and Files are separate permission sets.

---

# 5️⃣ **DATAFLOW GEN2 — The Brain of Data Ingestion**

The super-shortcut to master:

```
Dataflow Gen2 = M-language + Spark execution + Delta output
```

---

### MUST-REMEMBER EXAM RULES:

### ✔ Refresh succeeded but no data written?

→ **Destination (Append/Replace) missing**

### ✔ Duplicates every refresh?

→ Load mode = **Append** without filtering new rows.

### ✔ Cannot edit someone else’s Dataflow?

→ Missing **credential permission**.

### ✔ Queued long time?

→ **Capacity queue full**.

### ✔ Connecting to GitHub raw?

→ Needs **Anonymous** → blocked if disabled in tenant.

### ✔ Schema breaks after source change?

→ Sensitive steps:

```
Rename column
Merge queries referencing old names
Custom column referencing deleted fields
```

---

# 6️⃣ **PIPELINES — Fabric’s Orchestration Layer**

### Pipeline uses:

```
Spark (for notebooks)
SQL compute (for SQL scripts)
Data movement (for Copy)
Dataflow engine
```

### Core exam patterns:

### ✔ Pipeline cannot run?

→ Workspace in **Shared capacity**

### ✔ Pipeline retries fail immediately?

→ Workload disabled or capacity paused.

### ✔ Conditional execution not working?

→ Must use **If Condition** activity.

### ✔ Pipeline identity fails RLS?

→ Pipeline identity ≠ user identity.

---

# 7️⃣ **GOVERNANCE & SECURITY SHORTCUT GUIDE**

### 🔥 MOST IMPORTANT MEMORY SET:

```
Build permission → create reports, Analyze in Excel, reuse models.
Viewer → see only.
Contributor → edit and create items.
Admin → everything + settings.
```

### Sensitivity Label Scenarios:

If export/Copilot/sharing fails →
Always check:

```
Label: No Export
Label: Protected (encryption)
Downstream label application
Purview AI secure interactions
```

Remember:
**Protected labels block Publish to web + external share.**

---

# 8️⃣ **100 QUESTIONS → THE PATTERN BEHIND THEM**

If you understand the following decision tree, you can answer ALL 100 DP-600 admin questions:

---

### 🎯 **STEP 1 — Identify the category of the issue**

Ask yourself:

```
Is this user-level?
Is this workspace-level?
Is this capacity-level?
Is this tenant-level?
```

Examples:

**Fabric item missing → Tenant or Capacity**
**Slow performance → Capacity**
**Cannot share → Tenant (Sharing block)**
**Cannot find content → Discovery settings**
**Cannot export → Export settings**
**Cannot create workspace → Workspace creation setting**

---

### 🎯 **STEP 2 — Identify which workload**

```
Is it Spark? → Notebook? → Dataflow Gen2?
Is it SQL endpoint? → Warehouse?
Is it Power BI?
Is it Lakehouse?
Is it Pipelines?
```

Each workload has unique failure signatures.

---

### 🎯 **STEP 3 — Apply the right memory rule**

Use the rules from sections above:

* Files vs Tables
* Tenant vs capacity
* Build vs viewer
* Export vs view
* Shortcuts vs copies
* Schema drift behaviors

---

# 9️⃣ **REVISION MODE — 10 Second Memory Compression**

Here’s the **entire admin domain compressed into 10 seconds**:

```
Tenant = Policies (Fabric on/off, export, share, labels)
Capacity = Compute (Spark, Pipelines, queue, cache)
Workspace = Scope (who can edit/create + which capacity)
Lakehouse = Delta + Files + SQL endpoint + shortcuts
Dataflow = M + Spark + Delta output (Append/Replace)
Pipelines = Orchestration (Spark for notebooks)
Permissions = Build/Member/Contributor/Viewer
Labels = Export/sharing restrictions + AI governance
```

Memorize this block → You can solve 90% exam questions instantly.

---

# 🔟 **If you want, I can now provide:**

✔ A fully formatted **PDF-style notebook**
✔ A **mind-map** summary
✔ A **one-page cheat sheet**
✔ A **flowchart of admin troubleshooting**
✔ A **50-question rapid revision set** (compressed version)

Just tell me:

**“Give me the revision cheat sheet.”**
