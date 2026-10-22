# I built a workflow to keep component changes traceable across teams

> Component changes were already being made, but the context around them was scattered across Slack, Figma, email and conversations.

**Tags:** Shipped · Design System · Internal tool

| Field | Value |
| --- | --- |
| **Role** | Full end-to-end ownership |
| **Timeline** | 6 weeks |
| **Techniques** | Data analysis, benchmark, flow mapping, prototyping, user testing |
| **Tools** | Figma, Claude Code, GitHub, Slack |

> **[VISUAL — Hero cover]** Full-bleed background image with a device screen preview of the final plugin UI overlaid.

> **[NAV — Sticky side menu]** Six anchors: Problem · Discovery · Decisions · Solution · Impact · Learnings.

---

## Overview — A growing Design System with governance still taking shape

I'm part of a 3-person Design System team maintaining shared libraries across multiple products and brands, while product designers also evolve components inside their own UI Kits.

The Design System governance was still being defined, so ownership, change tracking and communication were not always consistent.

I owned this 6-week internal project end to end, from understanding the problem and testing possible workflows to designing and building the final solution.

---

## Problem — Information about component changes was getting lost

> **[VISUAL — QuestionsDiagram]** Diagram showing the recurring questions designers kept bringing to the Design System team (e.g. *"Which version should I use?"*, *"Has this component changed?"*, *"Why was this updated?"*).

Component changes happened across Design System libraries and product UI Kits, but the related information was spread across Slack, Figma files, emails and conversations.

When designers needed to understand what had changed, why, or which version to use, they often had to search across different sources or ask the Design System team.

> **[DATA CALLOUT — MetaBox variant="data"]**
> **TICKET ANALYSIS — 1 YEAR PERIOD**
> **12%** of **273** requests were related to **component changes** or which version to use.

> **[TRANSITION CALLOUT — warning variant]** "This impacted our work in two ways."

### The problems *(two warning callouts, side by side)*

**Time spent reconstructing past decisions** — *badge: TEAM DESIGN SYSTEM*
For the Design System team, each change had to be reconstructed from Slack, files and people every time the context was needed.

**Risk of outdated components and duplicated work** — *badge: TEAM UX/UI*
For product designers, limited visibility across projects created the risk of using outdated components or duplicating work already happening elsewhere.

> *Caveat (shown as a smaller note under the callouts):* I did not have enough data to measure how often outdated components were actually used, so I treated this as a risk rather than a measured outcome.

---

## Discovery — The existing process depended too much on people remembering it

### Mapping the workflow

I mapped how component changes were communicated between the Design System and product teams.

> **[VISUAL — Workflow diagram]** Caption: *"THE ACTUAL WORKFLOW AND THE MAJOR PAINT POINT"*. Diagram of the existing workflow between UX/UI and Design System teams highlighting the pain point (changes shared only with the person who requested them, so visibility never reached the rest of the teams).

A process already existed, but it relied on designers manually sharing updates through Slack, email or direct conversations. In practice, it was not followed consistently.

### Looking at existing approaches

I benchmarked **10 Design Systems** to understand how other teams tracked component changes.

Changelogs, release notes and documentation tools were the most common approaches, so I explored the options that could realistically work for us.

### Comparing the options with designers

I reviewed the most relevant approaches with the designers who would have to maintain them. The comparison highlighted three things that mattered:

### Our needs *(three info callouts with icons, side by side)*

- **Frictionless** *(lightning-bolt icon)* — The solution needs to fit into our teams' workflow, or it won't be adopted.
- **Retrievable** *(pin icon)* — Changes need to live somewhere stable and be easy to find later.
- **Proactive** *(paper-plane icon)* — Changes need to reach people, not just wait to be found.

Interviewing the designers who would maintain these tools surfaced a hard constraint: **adding another manual workflow would make adoption difficult.** Tools outside Figma offered better documentation, but introduced another place to maintain. Lighter Figma-based approaches reduced that friction, but gave us less control over how the information could be stored and reused.

> **[VISUAL — PrioritizationMatrix]** Interactive 2D matrix (X: *Outside workflow → Inside workflow*; Y: *Low retrievability → High retrievability*). Hover reveals pros/cons per option. Caption: *"HOVER ON EACH POINT TO SEE THE DETAILS"*. Items plotted:
> - **Track on Figma** *(bottom-right)* — ✓ Already in the workflow · ✕ Require to search manually each page (fails: proactive + retrievability)
> - **Figma Release Notes** *(mid-right, low-mid)* — ✓ Native in the tool · ✕ Not tied to individual components, and not searchable (fails: proactive + retrievability)
> - **Community Plugins** *(right, mid)* — ✓ Already integrated in Figma · ✕ None allowed to easily retrieve information (fails: proactive + retrievability)
> - **ZeroHeight** *(top-left)* — ✓ Changelog and release notes out of the box · ✕ Another touchpoint to maintain (fails: frictionless)
> - **Self-made Plugin — chosen solution** *(top-right, "sweet spot")* — ✓ Lives inside Figma, no context switch · ✓ Full control over how data is stored and queried · ✓ Communication can be automated

---

## Key decisions — Three decisions that shaped the final workflow

### 01. I moved from manual input to a guided form

The first versions relied too much on designers manually entering information, while automatic change detection was not reliable enough on complex files and could not capture the reason behind a change.

**Problem.** How could I reduce manual effort without losing the context only designers could provide?

**What I tested.**

> **[ACCORDION — three tabs]**

**Tab 1 — Manual table**
> *[Image: table under each component that designers filled in by hand.]*
A table under each component that designers filled in by hand. Designers filled in just the bare minimum, and often forgot key information.

**Tab 2 — Automatic detection**
> *[Image: change-detector prototype listing every node change with a per-row request to add context.]*
A script scanned files and detected changes automatically, then asked designers only for the missing context. On complex files it missed real changes and flagged meaningless ones. Even when it worked, it couldn't capture the "why", which only designers can give.

**Tab 3 — Guided form (chosen)**
> *[Video: short demo of the guided form inside the plugin.]*
**What changed.** A guided form inside the plugin walks designers through the information to log. Auto-fillable fields (component name, date, author) fill in on their own, while required fields keep data quality at 100%. Context the designer alone can provide — the reason for the change — stays as free input.

---

### 02. I added a sync queue to make the system status clear

During testing, designers were not always sure which changes had already been synchronised and which ones were still waiting to be sent.

**Problem.** The plugin did not give enough visibility over pending and synced changes, creating uncertainty during the workflow.

> **[TODO — Observation]** *What I observed.* Still to add: what designers did, where they hesitated and any errors or questions that emerged during testing of the pre-sync state.

> **[TODO — Asset]** *What changed — Sync queue.* Still to add: screenshot or short video of the Sync Queue in the plugin (list of pending changes, review flow, edit/remove entries before publishing).

---

### 03. I simplified the setup so designers could connect the plugin without technical support

The plugin needed to connect to the repository before it could be used, but the first setup required configuration steps that were not straightforward for non-technical users.

**Problem.** The initial onboarding created too much technical friction and could make designers dependent on the Design System team to start using the tool.

> **[TODO — Observation]** *What I observed.* Still to add: issues found during testing or rollout (steps that blocked non-technical designers, requests for help, errors during first-time setup).

> **[TODO — Asset]** *What changed — Simplified onboarding.* Still to add: screenshot or short video of the new onboarding flow (automated configuration, reduced steps, how the designer now connects without the Design System team's help).

---

## Technical decision — I chose a simpler architecture to ship within the project constraints

I explored different ways to store and retrieve the changelog data, including a single file, a structured GitHub repository and a RAG-based solution.

**Problem.** I needed a structure that was reliable enough for multiple designers, reusable for automation and realistic to implement within the six-week project without dedicated engineering support.

**Trade-off.**

> **[ACCORDION — three tabs]**

**Tab 1 — Single markdown file**
A single `.md` file on GitHub. Discarded due to slow file retrieval and overwrite issues when multiple designers edited at the same time.

**Tab 2 — RAG database**
A dedicated database with a Retrieval-Augmented Generation layer. Setup and maintenance cost (schema design, hosting, embeddings pipeline) was disproportionate to the phase of the project. Deferred for a later iteration once adoption and data volume justified the investment.

**Tab 3 — Structured folder on GitHub (chosen)**
> *[Video: short demo of the GitHub structure in use.]*
**Decision.** Sync the changelog to a structured folder on GitHub, one `.md` file per component, plus a "sync queue" inside the plugin. Fast, readable by humans and LLMs, and realistic to maintain within the project constraints — which keeps the door open for a retrieval layer later.

---

## Shipped solution — One workflow to capture, store and reuse component history

The final workflow connects the moment when a designer records a component change with the places where that information is later reused.

> **[STAGES — four cards in a 2×2 grid]**

| Stage | Description |
| --- | --- |
| **01 · Capture** | Designers record a component change through the Figma plugin. |
| **02 · Review** | Changes waiting to be synced remain visible so designers can check them before publishing. |
| **03 · Store** | The entries are saved in the shared GitHub structure, creating a history for each component. |
| **04 · Reuse** | The same information can be retrieved later and used to generate recurring communication such as weekly release notes. |

This means designers enter the context once instead of rewriting the same information for different channels.

> **[VISUAL — SolutionFlow]** Interactive flow diagram showing the designer's needs branching into *Add/Update component* and *Use component*, converging into a single synced source of truth, and fanning out into three outcomes: *Fast search of past changes*, *Team aligned via release notes*, *Team aligned via smart reminders*. Each node is clickable and opens a modal with a screenshot/video and short description.

> **[TODO — Asset]** *Solution carousel.* Still to add: one image per stage (Capture, Review, Store, Reuse) — plugin form, sync queue, GitHub folder, weekly release note.

---

## Impact — The workflow created a shared history for component changes

The project moved component history from scattered conversations into one structured workflow. For the Design System team, recorded changes no longer need to be reconstructed from Slack, files and people every time the context is needed. The structured data also removed part of the manual work involved in preparing release communication.

> **[BENTO — four impact cards in an asymmetric 3-column grid]**
> Row 1: *Source of truth* (wide, success) + *Recover change context* (info)
> Row 2: *Prepare release notes* (info) + *Team adoption* (wide, success)

| Card | After | Before |
| --- | --- | --- |
| **Source of truth** | **1** | Not available. Split between Slack, emails, people. |
| **Recover change context** | **~5 min** | Up to 1 working day. |
| **Prepare release notes** | **~25 min** | ~4h of manual work. |
| **Team adoption** | **6 / 8** | Designers that logged at least 1 change in the past 30 days. |

### Still to measure — expected at Q2 *(two neutral cards)*

| Card | Target | Note |
| --- | --- | --- |
| **Similar tickets** | **−70%** | Expected reduction: to re-run the same Slack ticket analysis at Q2. |
| **Rework on delivered flows** | **Baseline** | To set at Q2: track hours spent replacing outdated components in delivered flows to establish a baseline. |

---

## Limitation — Retrieval is getting slower as the history grows

The GitHub structure was a good fit for the first release because it was simple, transparent and easy to maintain.

As the number of logs grows, retrieval is starting to slow down. At this scale, the RAG approach I initially deferred would now be worth reconsidering as a retrieval layer on top of the existing source of truth.

---

## Learnings — What I would carry into the next iteration

1. **Adoption is part of the design problem.**
   A better documentation tool does not help if maintaining it adds too much work to the existing workflow.

2. **Structured data made automation useful.**
   Release notes and retrieval became easier only after the component history had a consistent structure.

3. **The right technical choice can change over time.**
   The repository was enough for the first release. As the amount of data grows, the trade-off is changing and a dedicated retrieval layer now makes more sense.

---

## Open TODOs for the auditor's awareness

Sections that are **content-complete** and ready for review:
- Overview · Problem · Discovery · Technical decision · Shipped solution (text) · Impact · Limitation · Learnings
- Key decision 01 (Guided form)

Sections where **copy + assets are still placeholders** (clearly marked in the page with yellow "TODO" boxes):
- Key decision 02 — Sync queue: *What I observed* copy + Sync queue asset
- Key decision 03 — Simplified setup: *What I observed* copy + Onboarding asset
- Shipped solution — carousel of stage screenshots
