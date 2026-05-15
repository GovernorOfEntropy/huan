# The Death of Drift: A HUAN Architecture for Post-SaaS Governance

**Status:** Draft
**huan-compliant:** false
**Type:** Whitepaper
**License:** Apache 2.0
**Drafted:** 2026-05-15

---

## Irreducible Concept

Every organization suffers from drift — the widening gap between strategic intent, technical reality, and documentation. Traditional fixes add process, which does not scale. HUAN is an open standard for dual-audience documentation that kills drift at the source: every artifact serves humans and AI simultaneously, coherence is a computable graph property, and a surgeon-agent heals the corpus before anyone notices the wound. This isn't a documentation tool. It is the immune system for the corporate brain.

---

## I. The Crisis of Institutional Entropy

### The Drift Trap

Drift is not a bug. It is the default. Every organization experiences the widening gap between what leadership believes, what engineering built, and what the documentation says. The API spec says timeout_ms: 30000. The README says "uses 30-second timeout." The code uses config.get('request_timeout'). Three sources. One concept. Zero agreement.

The traditional fix has been process — more reviews, more gates, more meetings. Process does not scale. Every gate adds latency. Every review consumes attention. The organization spends more time verifying coherence than producing value.

### The Translation Tax

Systems that separate human-readable prose from machine-readable data impose a translation tax. Every time an engineer reads an API spec and translates it into code, the tax is paid. Every time a product manager updates a wiki page that's already stale, the tax is paid. The tax compounds. Large organizations spend 20-30% of engineering time on coherence maintenance — verifying that what's written matches what's built.

HUAN kills the tax at the source. One card. Two audiences. No duplication. The Irreducible Concept is human-readable prose. The Irreducible Context is AI-readable operational data. Both live in the same artifact. Neither can be removed without breaking the card.

### The Cost of Memory Loss

Institutional memory is the most expensive thing an enterprise loses every day. Engineers leave. Wikis rot. READMEs go unread. The organization forgets why decisions were made. Without the reasoning, future decisions are made in the dark.

A HUAN corpus preserves the why alongside the what. Every card carries its provenance — source paths, dependency chains, version history. The corpus is the company's git log of thinking.

---

## II. The HUAN Standard: Atomic Intelligence

### The Dual-Audience Invariant

Every HUAN artifact is a single file carrying two structurally separated sections:

- **Irreducible Concept** — Human-readable. Prose, narrative, philosophy. The "why." A founder, engineer, or product manager reads this to understand what the card means.

- **Irreducible Context** — AI-readable. Source paths, dependencies, versions, operational metadata. An AI role (Builder, Tester, Analyst) reads this to understand what the card requires to act.

Separation is structural, not physical. One artifact. Two audiences. Zero translation.

Named for Huan, Hound of Valinor, who understood every tongue and spoke only when it mattered. A card that is not dual-audience is not a HUAN card.

### One Subject, One Card

Atomicity kills context sprawl at the source. Each card covers exactly one subject. Cross-references (wiki-links) create edges between cards, forming a navigable graph. The graph is the structure. The cards are the content.

### Protocol Over Platform

HUAN is an open I/O contract — a standard, not a product. The standard defines seams. Implementations compete on rendering, interaction, and layout quality.

Jepson is the reference runtime — the first implementation. It proves the standard is implementable. It is not required. Any tool that reads and writes HUAN-compliant cards is a valid HUAN implementation.

---

## III. The Immune System: Computable Coherence

### The Safety Net Hierarchy

Four layers of defense against drift:

1. **Git** — protects against code loss. Version history. Rollback.
2. **Lifecycle** — protects against stale cards. Formal state machine: seed → growing → HUAN → pruned. Every transition is gated. The mdwiki 2-way edge rule blocks promotion to HUAN unless all cross-references reciprocate.
3. **Analyst** — protects against coherence drift. Scans the card graph for six tension types: concept/context mismatch, stale references, one-way edges, orphan cards, circular dependencies, version skew. Produces structured Tension Reports.
4. **Surgeon** — protects against accumulation of unfixed tensions. Reads analyst reports. Auto-fixes deterministic problems. Proposes strategic changes for human review. Escalates what it cannot fix.

### The Pulse: Diagnostic

Real-time monitoring via NDJSON event streams. Eight dimensions of card health: staleness, path rot, tension, orphan status, circular dependency, version skew, broken cross-references, coherence drift. Every dimension carries severity (info/warning/error/critical) and remediation hints.

### The Intelligence: Analyst

The analyst moves documentation quality from "I read it and it seems fine" to "the graph has zero coherence violations." Tension becomes a computable property. A card claiming huan-compliant: true but carrying a concept/context mismatch is detectably broken. The analyst doesn't read. It computes.

### The 2-Way Edge Rule

Visual diagrams are valid only if the underlying card graph relationships are bidirectional. A diagram showing A connects to B is correct only if card A references card B and card B references card A. Diagram correctness is a graph property, not a visual one. No separate diagram language required — the card graph IS the diagram source.

---

## IV. Surgical Remediation: Closing the Loop

### The Surgeon Role

huan-surgeon closes the loop the analyst opens. Named for Huan's decisive action — deep knowledge and surgical precision in one being. The surgeon reads analyst tension reports, accesses the full corpus, and applies the minimum intervention.

### Autonomy Levels

| Action | Autonomy |
|--------|----------|
| Fix stale file paths | Auto |
| Bump version references | Auto |
| Fix wiki-link formatting | Auto |
| Split hybrid cards | Propose (human review) |
| Merge duplicate cards | Propose (human review) |
| Create cross-references | Propose (human review) |
| Delete a card | NEVER |
| Prune a card | NEVER (human-gated) |

Every auto-fix action is logged with before/after snapshot and rollback path. Git is the safety net — high-velocity autonomous maintenance with permanent undo.

---

## V. Governance at the Speed of AI

### Beyond Code Review

Traditional governance reviews code. HUAN governance reviews structural coherence — the entire graph of what the organization believes to be true. The question shifts from "does this code work?" to "does this organization's stated intent match its operational reality?"

### Deprecation Propagation

When a card is pruned, the signal propagates automatically. All cards referencing the pruned card are flagged. Dependents are notified. The Steward reviews. Propagation cascades up to 3 hops. The organization knows immediately what a change affects — not by reading documentation, but by watching the graph.

### The Vision

A low-entropy organization where the distance between "what we think" and "what is true" remains zero. Where the Analyst audits the corpus for contradictions before they become incidents. Where the Surgeon fixes what's broken before anyone notices. Where the founder thinks. Where the factory builds.

**This is not a documentation tool. It is the immune system for the corporate brain.**

---

## Irreducible Context

- Source: huan-spec v1.0.2, huan-lifecycle v1.0.0, huan-analyst v1.0.0, huan-surgeon v1.0.0, huan-diagnostic v1.0.0, huan-visual v1.0.0
- Dependencies: ZK-099 (Coherence as Quality of Life), ZK-111 (Context Sprawl Is the New Monolith)
- References: docs/huan-standard/hpe-submission-package.md

---

*Lv25:10*
