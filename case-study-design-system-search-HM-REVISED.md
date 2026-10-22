# I built a workflow to keep component changes traceable across teams

> Component changes were already happening across Design System libraries and product UI Kits, but the context around them was scattered across Slack, Figma, email and conversations.

**Shipped · Design System · Internal tool**

| Field | Value |
| --- | --- |
| **Role** | Full end-to-end ownership |
| **Timeline** | 6 weeks |
| **Techniques** | Data analysis, benchmark, flow mapping, prototyping, user testing |
| **Tools** | Figma, Claude Code, GitHub, Slack |

> **[VISUAL — Hero cover]** Keep the final plugin UI as the main visual. Do not add architecture or feature details here.

> **[NAV — Sticky side menu]** Problem · Discovery · Decisions · Solution · Impact · Learnings

---

## Overview — A growing Design System with governance still taking shape

I'm part of a 3-person Design System team maintaining shared libraries across multiple products and brands. Product designers also evolve components inside their own UI Kits.

Governance was still being defined, so ownership, change tracking and communication were not always consistent. I owned this 6-week internal project end to end, from understanding the problem and testing workflows to designing and building the final solution.

> **[VISUAL — Existing team / library diagram]** Reuse the current diagram that shows the relationship between the Design System team, shared libraries and product UI Kits. Keep it small. It only needs to explain where component changes can happen.

---

## Problem — Information about component changes was getting lost

> **[VISUAL — QuestionsDiagram]** Keep the recurring questions as the opening visual:
> *Which version should I use?* · *Has this component changed?* · *Why was this updated?*

Component changes happened across Design System libraries and product UI Kits, but the related information was spread across Slack, Figma files, emails and conversations.

When designers needed to understand what had changed, why, or which version to use, they often had to search across different sources or ask the Design System team.

> **[DATA CALLOUT]**
> **12% of 273 requests** reviewed over one year were related to component changes or version questions.

### This created two problems

**Design System team · Time spent reconstructing decisions**  
Past changes had to be pieced together from messages, files and people whenever the original context was missing.

**UX/UI team · Limited visibility across projects**  
Designers could miss changes happening elsewhere, increasing the risk of using an outdated component or duplicating work already done in another project.

> **[SMALL NOTE]** I did not have enough data to measure how often outdated components were actually used, so I treated this as a risk rather than a measured outcome.

---

## Discovery — I looked at the workflow before choosing a solution

### Mapping where information was getting lost

I mapped how component changes were communicated between the Design System and product teams.

A process already existed, but it relied on people manually sharing updates through Slack, email or direct conversations. In practice, it was not followed consistently.

> **[VISUAL — Existing workflow]** Reuse the current workflow diagram. Highlight one point only: changes often stayed visible to the people involved in the original request instead of reaching the wider team.

### Looking at how other teams handled it

I benchmarked **10 Design Systems** to understand how they tracked component changes.

Changelogs, release notes and documentation tools were the most common patterns, so I shortlisted the options that could realistically work in our context.

> **[VISUAL — Benchmark]** Reuse the current benchmark visual, but keep it secondary. The benchmark supports the decision; it is not the main story.

### Comparing the options with designers

I reviewed the most relevant approaches with the designers who would have to maintain them.

Three criteria became important:

- **Frictionless** — it had to fit the existing workflow or adoption would be difficult.
- **Retrievable** — past changes needed a stable place where they could be found later.
- **Proactive** — important changes needed to reach people, not just wait to be searched for.

Testing also surfaced a practical constraint: **adding another manual workflow would make adoption difficult.**

Tools outside Figma offered better documentation, but introduced another place to maintain. Lighter Figma-based approaches reduced that friction, but offered less control over how the information could be stored and reused.

> **[VISUAL — PrioritizationMatrix]** Reuse the current matrix here. Let the visual do most of the comparison work.
>
> Keep only these short labels in the page copy:
> - Track on Figma
> - Figma Release Notes
> - Community Plugins
> - Zeroheight
> - Custom Plugin
>
> The custom plugin should appear as the outcome of the comparison, not as an answer that was obvious from the start.

---

## Key decisions — Three UX decisions shaped the workflow

### 01. I replaced free-form input with a guided flow

The first versions relied too much on designers remembering what to document.

I tested three approaches: a manual table, automatic change detection and a guided form.

> **[ACCORDION — 3 tabs]**
>
> **Manual table**  
> Designers entered only the minimum information and often missed useful context.
>
> **Automatic detection**  
> On complex files it missed meaningful changes, flagged irrelevant edits and still could not capture why a change had been made.
>
> **Guided form · chosen**  
> The plugin asks designers only for information that requires their context. Component name, date and author can be filled automatically, while the reason for the change stays as user input.

**Decision:** use a guided flow that reduces effort without removing the context only designers can provide.

---

### 02. I added a sync queue to make status visible

During testing, designers were not always sure which changes had already been synced and which ones were still pending.

That uncertainty made it harder to understand whether an entry still needed action and increased the risk of duplicate or missed updates.

> **[TODO — Observation]** Add the clearest behaviour seen during testing. Keep it to 1–2 sentences.
>
> **[TODO — Asset]** Add a screenshot or short video of the Sync Queue showing pending entries and the ability to review, edit or remove them before syncing.

**Decision:** make pending work visible before sync, so designers can understand the system status and review changes before publishing.

---

### 03. I simplified setup so designers could start without technical support

The plugin needed to connect to the repository before it could be used, but the first setup required configuration steps that were not clear to non-technical users.

This created unnecessary dependency on the Design System team during onboarding.

> **[TODO — Observation]** Add the main issue seen during rollout or testing. Avoid listing every setup problem.
>
> **[TODO — Asset]** Add a before / after of the setup flow or a short video of the simplified onboarding.

**Decision:** reduce the setup to the minimum information designers need and automate configuration wherever possible.

---

## Technical trade-off — I chose an architecture I could realistically ship

I explored three ways to store and retrieve the changelog data.

> **[ACCORDION — 3 tabs]**
>
> **Single Markdown file**  
> Simple to implement, but concurrent edits created overwrite issues and retrieval became inefficient.
>
> **RAG database**  
> Better suited to semantic retrieval at scale, but the setup and maintenance cost was too high for the first release.
>
> **Structured GitHub repository · chosen**  
> One Markdown file per component. It was readable, reusable and realistic to maintain within the six-week project.

**Decision:** use the simplest structure that solved the current reliability problem and keep the option to add a retrieval layer later.

This trade-off becomes important again in the limitation section.

---

## Shipped solution — One flow to capture, review and reuse component history

The final workflow connects four steps.

| Stage | What happens |
| --- | --- |
| **01 · Capture** | Designers log a component change through the Figma plugin. |
| **02 · Review** | Pending entries remain visible in the Sync Queue before publishing. |
| **03 · Store** | Changes are synced to the shared GitHub structure, creating a history for each component. |
| **04 · Reuse** | The same data can be retrieved later and used to prepare weekly release notes. |

Designers enter the context once instead of rewriting the same information for different channels.

> **[VISUAL — SolutionFlow]** Adapt the current final flow and show only what was actually shipped:
>
> **Figma → Guided input → Sync Queue → GitHub → History retrieval / Release notes**
>
> Remove smart reminders, automatic component metadata and any other feature that was not shipped.
>
> **[OPTIONAL CAROUSEL]** One real screenshot per stage: form, Sync Queue, GitHub structure, release note. Use this only if it adds clarity beyond the main flow.

---

## Impact — The workflow gave component changes a shared history

The project moved component history from scattered conversations into one structured workflow.

> **[BENTO — Keep 4 cards. Lead with the outcome, then the operational metrics.]**

| Outcome | After | Before |
| --- | --- | --- |
| **Shared source of truth** | **1 structured source** | Split across Slack, email, files and people |
| **Recover change context** | **~5 min** | Up to 1 working day |
| **Prepare release notes** | **~25 min** | ~4h of manual work |
| **Active adoption** | **6 / 8 designers** | Logged at least one change in the last 30 days |

After launch, one product designer also mapped the components in their UI Kit and continued maintaining their history through the plugin.

### What I still need to measure

- whether repeated Design System requests decrease over time
- whether the workflow reduces outdated component usage in delivered flows

> Do not show expected percentage reductions here unless they are based on measured evidence. The open questions are enough.

---

## Limitation — Retrieval is getting slower as the history grows

The GitHub structure was a good fit for the first release because it was simple, transparent and easy to maintain.

As the number of logs grows, retrieval is becoming slower.

At this scale, the RAG approach I initially deferred would now be worth reconsidering as a retrieval layer on top of the existing source of truth.

> **[SMALL VISUAL — optional]**
> Current: GitHub structured history → direct retrieval  
> Next scale: GitHub structured history → retrieval layer → semantic search

---

## Next — What I would validate next

These ideas came out of the project but were **not shipped or validated**.

### Component status
Surface version or release information closer to the component.

### Release reminders
Notify designers about upcoming component releases or replacements.

### Proactive updates
Surface changes that may be relevant to the product a designer is working on.

> **[VISUAL — Concepts, not shipped]** Reuse the concepts you already created, but clearly label the entire block **CONCEPTS, NOT SHIPPED**.

---

## Learnings — What I would carry into the next iteration

1. **Adoption is part of the design problem.**  
   A better documentation tool does not help if maintaining it adds too much work to the existing workflow.

2. **Structured data made automation useful.**  
   Release notes and retrieval became easier only after component history had a consistent structure.

3. **The right technical choice can change over time.**  
   The repository was enough for the first release. As the amount of data grows, the trade-off is changing and a dedicated retrieval layer now makes more sense.
