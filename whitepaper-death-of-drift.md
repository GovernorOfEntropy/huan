---
title: "The Death of Drift: HUAN Architecture for Post-SaaS Governance"
status: Draft
version: 1.3.0
huan-compliant: false
type: Whitepaper
license: Apache 2.0
drafted: 2026-05-15
updated: 2026-05-16
versions:
  - version: "1.3.0"
    date: "2026-05-16"
    changes: "Added section 5: The Bridge — Human-to-Role Retrieval. Generalized internal role names (Builder→implementation role, Tester→validation role, Steward→maintainer). Removed Jepson and HPE submission references. Section numbering corrected (1–10 continuous). Neutralized for perpetual standalone publication."
  - version: "1.2.0"
    date: "2026-05-16"
    changes: "Added section 7: The Directory Is the Perimeter — README as frontmatter, directory-manifest, untracked detection, version lockout, domain scoping. Pillar version references updated to current (spec 1.0.4, analyst 1.1.0, surgeon 1.1.0, lifecycle 1.0.3). Sections renumbered 7→10."
  - version: "1.1.0"
    date: "2026-05-16"
    changes: "Added section 3: The Spec Is a Distillation — observation-driven design. HUAN acronym expansion. Lifecycle references updated to v1.0.2. Sections renumbered 3→9."
  - version: "1.0.0"
    date: "2026-05-15"
    changes: "Initial draft. 8-pillar architecture, dual-audience thesis, computable coherence, surgeon remediation, deprecation propagation."
audience: practitioner
---

**Note:** This is a whitepaper, not a HUAN card. `huan-compliant: false`. For the standard, see huan-spec v1.0.5.

## Irreducible Concept

The industry has accepted a quiet failure as permanent. Every organization drifts — the gap between what leadership believes, what engineering built, and what documentation says widens daily. The accepted response is process. More reviews. More gates. More meetings. The architecture of the response matches the architecture of the problem: both are human-scale. Drift moves faster than humans can.

We built HUAN — Hybrid Universal Artifact Notation — to break that cycle. It is an open standard for dual-audience documentation. Every artifact serves humans and AI simultaneously. Coherence is a computable graph property — not a feeling, not a review finding. A surgeon-agent heals the corpus before anyone notices the wound. The founder thinks. The factory builds. Drift arrives. The system responds.

This is not a documentation tool. It is the immune system for the corporate brain. We are putting it in the world because the problem deserves a response at its own scale.

---

## 1. Drift Arrives Quietly

No organization starts with drift. Every organization acquires it.

The API spec says `timeout_ms: 30000`. The README says "uses 30-second timeout." The code calls `config.get('request_timeout')`. Three sources. One concept. Zero agreement. Nobody broke anything. The drift arrived between commits — between the spec review and the sprint planning, between the deploy and the postmortem.

The industry treats this as cost of doing business. Documentation ages. Wikis rot. Engineers leave and take the why with them. The organization forgets decisions. Future decisions are made without the reasoning that produced the original ones. The cost compounds. It is not measured on a balance sheet because the industry has no instrument for it.

Process is the standard answer. More gates. More checklists. More meetings to verify that what's written matches what's built. This is a category error. Drift is not a process problem with a process solution. Drift is a structural problem. Process adds surface area for drift to hide behind. Every gate becomes a ceremony. Every review becomes theater. The organization spends more time verifying coherence than producing value — and still drifts.

We built a structural answer. Drift is the default state of any organization without an immune system. HUAN is the immune system.

---

## 2. Humans and Machines Speak Different Languages

The industry separates human-readable prose from machine-readable data. Specs for people. APIs for machines. Two artifacts. One truth. Every handoff between them pays a tax.

An engineer reads an API spec. Translates it into code. The code ships. The spec ages. The README diverges. Three artifacts. One truth. The tax compounds with every translation.

Large organizations running documentation estates at scale burn 20-30% of engineering time on coherence maintenance — chasing stale references, reconciling contradictory sources, verifying what's written against what's built. This is not documentation work. This is the cost of accepting that humans and machines cannot share a single artifact. The industry pays it because the industry believes it is inevitable.

It is not. HUAN kills the translation tax at the artifact level. One card carries two structurally separated sections. The Irreducible Concept is human-readable prose — the reason the card exists. The Irreducible Context is AI-readable operational data — the dependencies, the versions, the paths. Both live in the same file. Neither can be removed without breaking the card. One source. One truth. Zero translation.

The format is atomic. Each card covers exactly one subject. Cross-references form edges between cards. The edges create a navigable graph. The graph is the structure. The cards are the content.

HUAN is a standard, not a platform. It defines I/O contracts at the seams. Implementations — a reference runtime, third-party tooling, custom renderers — compete on what happens inside the seam. The reference runtime proves the standard is implementable. It is not required. Any tool that reads and writes HUAN-compliant cards is a valid HUAN implementation. We built the standard to be adopted, not to be owned.

---

## 3. The Spec Is a Distillation

The spec was built on observing the problem.

You did not design HUAN in a vacuum. You watched the factory work. You saw where tension accumulated — one-way edges, stale references, orphan cards, version skew. And you wrote the spec to make those tensions visible.

The spec is not a theory. It is a distillation.

Every field in the frontmatter exists because something broke without it. Every rule in the authoring discipline exists because a card drifted. Every transition in the lifecycle exists because a card aged out and nobody noticed.

HUAN did not start as a white paper. It started as a factory that built things from prompts against contracts. The factory produced code. The code produced tension. The tension revealed what the documentation was missing. The spec closed the gap.

This is the method. Build. Observe the failure. Write the rule. Repeat. The 8 pillars are not a design. They are 8 things that broke and then got fixed.

---

## 4. Coherence Is a Graph Property

HUAN moves documentation quality from subjective review to measurable property. The question shifts from "does this look right?" to "does the graph have zero coherence violations?"

The analyst (huan-analyst v1.1.1) scans the card graph for six tension types.

| Tension | Detection | Severity |
|---------|----------|----------|
| Concept/Context mismatch | Semantic conflict between prose and operational data | Critical |
| Stale references | Referenced paths do not resolve on disk | Error at HUAN status |
| One-way edges | Card A references B but B does not reference A | Blocks growing→HUAN transition |
| Orphan cards | Zero inbound references from any other card | Warning |
| Circular dependencies | Reference chain forms a cycle | Error |
| Version skew | Referenced version is outdated | Warning |

The analyst does not read. It computes. A card claiming `huan-compliant: true `while carrying a concept/context mismatch is detectably broken. The tension is not an opinion. It is a structural property of the graph. This is the shift: coherence stops being something you audit and becomes something you measure.

The diagnostic layer (huan-diagnostic v1.0.1) monitors eight dimensions of card health. NDJSON event streams. Every dimension carries severity and a remediation hint. The visual layer (huan-visual v1.0.1) generates diagrams from the card graph. The 2-way edge rule enforces correctness: a diagram showing A connects to B is valid only if card A references B and card B references A. Diagram correctness is a graph property, not a visual one. No separate diagramming language required — the card graph is the diagram source.

---

## 5. The Bridge: Human-to-Role Retrieval

Dual-audience cards are inert without a way to find them. The Human-to-Role retrieval pipeline (huan-h2r v1.0.1) is the bridge between a human question and the right cards.

A human asks a question in natural language. The pipeline decomposes it into search primitives — entity, action, scope, depth. It traverses the card graph from the query's entry points. It scores retrieved cards by concept match, graph distance, and status. It assembles a retrieval package within a declared token budget and delivers it to the requesting AI role.

The pipeline is role-aware. An implementation role gets code-generation cards only. A validation role gets test contracts. An analysis role gets the full graph. Role awareness is not security — it is context isolation. Each role sees what it needs and nothing more. Context pollution degrades output quality. The retrieval pipeline prevents it.

The fallback chain preserves corpus integrity. If no card directly answers, the pipeline reports "no match" rather than fabricating from partial context. Silence is better than noise. Unmatched queries are logged for maintainer review. The corpus learns what it doesn't know.

---

## 6. Four Layers. No Single Point of Failure.

Drift attacks at every layer. HUAN defends at every layer. No single mechanism carries the full burden.

| Layer | Mechanism | What It Protects |
|-------|-----------|-----------------|
| 1 | Git | Code loss. Version history. Rollback. |
| 2 | huan-lifecycle v1.0.4 | Stale cards. Formal state machine from seed to pruned. Every transition gated. |
| 3 | huan-analyst v1.1.1 | Coherence drift. Six-tension scan. Structured reports. |
| 4 | huan-surgeon v1.1.1 | Accumulated unfixed tensions. Surgical remediation at three autonomy levels. |

Each layer catches what the layer below cannot. Git catches code loss but accepts stale documentation. The lifecycle catches staleness but does not detect semantic mismatch. The analyst detects mismatch but does not act on it. The surgeon closes the loop.

The lifecycle state machine (huan-lifecycle v1.0.4) is the structural defense. A card cannot advance from growing to HUAN status unless all cross-references reciprocate. A card at HUAN status cannot be modified without triggering re-evaluation. The gates are not advisory. They are encoded in the state transitions.

Deprecation propagates automatically. Prune a card. The signal moves. Every dependent is flagged within three hops. The organization knows immediately what a change affects — not by reading documentation, but by watching the graph respond. The change becomes visible at the speed of the graph, not the speed of the next meeting.

---

## 7. The Directory Is the Perimeter

Every HUAN chapter is a directory. Every directory carries a README. That README is not documentation. It is the perimeter.

The directory-manifest is the indexed inventory of everything in the chapter — every spec, every skill file, every whitepaper, every card. The analyst's first pass does not read content. It compares the manifest against what is actually on disk.

- File listed in manifest but missing → stale reference. Coherence violation.
- File on disk but not in manifest → unmapped entity. Flagged immediately.
- File version on disk does not match manifest → version skew. Pipeline locks.

This is deterministic. No content analysis. No AI judgment. List comparison. Instant audit. Every directory self-audits on every scan.

This turns a file folder into an object-oriented database primitive. The folder knows its own contents, enforces its own version boundaries, and computes its own structural health through a single file.

**Zero untracked elements.** The directory is not HUAN-compliant until every file is either in the manifest or removed. An engineer drops a file without updating the README — flagged. An external process writes a log file — flagged. The perimeter is absolute. What is not declared does not belong.

**Version lockout.** The manifest declares expected versions. If a file carries `version: 1.0.4` in its frontmatter but the manifest says `version: 1.0.2`, the pipeline locks. No artifacts in the directory advance. The lock is per-directory — a breach in one chapter does not cascade. The lock persists until the manifest is updated or the file version corrected.

**Domain-scoped.** The analyst and surgeon operate at the chapter level by default. A chapter PM deploys their own instances. The analyst scans only the chapter's README and artifacts. The surgeon fixes only within the chapter's perimeter. Full-corpus access requires explicit maintainer approval. Scans stay fast, findings stay relevant, ownership stays clear.

The directory becomes a fort. The README is the gate. The manifest is the guard tower. The analyst is the watch. The pipeline obeys the perimeter. Drift arrives at the directory boundary and is turned back before it enters.

---

## 8. The Surgeon

huan-surgeon v1.1.1 closes the loop the analyst opens. 

The surgeon reads analyst tension reports. Accesses the full corpus. Applies the minimum intervention. It does not design. It does not decide strategic direction. It executes the smallest change that closes a specific tension.

| Action | Autonomy | Gate |
|--------|---------|------|
| Fix stale file paths | Auto | None |
| Bump version references | Auto | None |
| Fix wiki-link formatting | Auto | None |
| Split hybrid cards | Propose | maintainer approval |
| Merge duplicate cards | Propose | maintainer approval |
| Create cross-references | Propose | maintainer approval |
| Delete a card | NEVER | — |
| Prune a card | NEVER | Human-gated |

Every auto-fix logs: timestamp, card affected, change made, before/after snapshot, rollback path, rationale. Git is the safety net. High-velocity autonomous maintenance. Permanent undo.

The surgeon's autonomy model is calibrated. Deterministic fixes — stale paths, version bumps, formatting — execute without review. The machine is faster and more reliable at these than a human. Strategic changes — splitting hybrid cards, merging duplicates, creating new cross-references — require human approval. The machine proposes. The human decides. Changes with irreversible consequence — deletion, pruning — are never automated. The line between machine speed and human judgment is explicit and enforced.

---

## 9. What We Built and What It Means

We built an 8-pillar architecture. Every pillar is drafted. Every pillar carries a version. The artifacts exist, the contracts are defined, the reference runtime is implemented.

The pillars:
- **huan-spec v1.0.5** — atomic card format. The foundation.
- **huan-skill v1.0.3** — the HUAN product definition. This standard, managed.
- **huan-lifecycle v1.0.4** — state machine from seed to pruned. Deprecation propagation.
- **huan-h2r v1.0.1** — human-to-role retrieval pipeline.
- **huan-diagnostic v1.0.1** — card health monitoring. NDJSON events.
- **huan-visual v1.0.1** — card graph to diagram rendering. 2-way edge rule enforced.
- **huan-analyst v1.1.1** — tension detection as computable graph property.
- **huan-surgeon v1.1.1** — agentic remediation. Surgical, calibrated, auditable.

The architecture is complete. The standard is open. The reference implementation exists. What remains is adoption, feedback, and iteration — the work of a living standard.

---

## 10. The Immune System

The distance between what an organization thinks it knows and what is actually true is its entropy budget. High-entropy organizations spend that budget on meetings, reviews, and incident remediation — paying the tax the industry has accepted as permanent. Low-entropy organizations spend it on building.

HUAN closes the gap by making coherence a machine problem. The analyst audits the corpus for contradictions before they become incidents. The surgeon fixes what's broken before anyone notices. The lifecycle gates prevent decay from entering the system. The founder thinks. The factory builds. Drift arrives. The system responds. Silence is the baseline.

We built this because the problem deserved better than process. The industry has lived with drift long enough to forget it is optional. It is optional. We proved it. The standard is open. The reference runtime ships. The architecture is eight pillars, drafted, versioned, and free.

**This is not a documentation tool. It is the immune system for the corporate brain.**

---

## Irreducible Context

- Source: huan-spec v1.0.5, huan-lifecycle v1.0.4, huan-analyst v1.1.1, huan-surgeon v1.1.1, huan-diagnostic v1.0.1, huan-visual v1.0.1, huan-h2r v1.0.1
- Dependencies: huan-spec v1.0.5 (atomic card format, core standard inherited by all pillars)
- Implementation: Reference runtime available. Any conforming implementation is valid.

---

*Lv25:10*
