Skip to content
Navigation Menu
gatagit
snowagents

Type / to search
Code
Issues
Pull requests
Actions
Projects
Wiki
Security
Insights
Settings
You only have a single verified email address. We recommend verifying at least one more email address to ensure you can recover your account if you lose access to your primary email.


snowagents
/snowcmdbagentflow
Go to file
t
gatagit
gatagit
Create snowcmdbagentflow
03babda
 · 
now

Code

Blame
53 lines (45 loc) · 1.04 KB
flowchart TD
  subgraph User & Governance
    U[CMDB Manager / CAB]
    GOV[Policies & Naming Standards]
  end

  subgraph ServiceNow Platform
    UI[Cleanup Dashboard (Now/PA)]
    LOGS[Audit Logs & Rollback]
    CMDB[(CMDB)]
    FD[Flow Designer / IH]
  end

  subgraph Multi-Agent Orchestrator
    PLAN[🧭 Planner\n(goal decomposition)]
    DEDUP[🧹 Dedup Agent\n(similarity, keys)]
    NORM[🧱 Normalizer Agent\n(naming rules)]
    REL[🔗 Relationship Agent\n(dep mapping)]
    VAL[✅ Validator Agent\n(policy & risk)]
    RAG[📚 RAG/Rules Retriever\n(standards, SOPs)]
  end

  subgraph External Sources
    SCCM[SCCM / MECM]
    DISC[SN Discovery]
    ASSET[AssetTrack / WASP]
  end

  U -->|review/approve| UI
  GOV --> RAG
  UI --> PLAN

  PLAN --> DEDUP
  PLAN --> NORM
  PLAN --> REL
  DEDUP --> VAL
  NORM --> VAL
  REL --> VAL
  VAL -->|approved auto-fix| FD
  VAL -->|needs human| UI

  FD --> CMDB
  CMDB --> UI
  FD --> LOGS
  VAL --> LOGS

  SCCM --> DEDUP
  DISC --> DEDUP
  ASSET --> DEDUP

  NORM --> RAG
  REL --> CMDB
  DEDUP --> CMDB
snowagents/snowcmdbagentflow at main · gatagit/snowagentsWhile the code is focused, press Alt+F1 for a menu of operations.
