# HUAN — HPE Open Source Submission Package

**Status:** Draft — Phase 5 of Advisor directive (2026-05-15)
**Prepared by:** Steward (HAIRY)
**Owner:** HUAN PM (FL-022)
**Legal entity:** Deferred (ZK-081)

---

## Overview

HUAN is an 8-pillar architecture suite for dual-audience (human + AI) documentation. Five concepts within the architecture are potentially patentable and are submitted for HPE open-source review prior to public release.

The standard defines input/output contracts. Implementations compete on rendering, interaction, and layout quality. The platform wins by defining seams, leaving the middle open.

**Dependency chain:** HUAN (standard) → Jepson (factory, reference runtime) → downstream products

---

## Concept 1 — Dual-Audience Atomic Format

### Summary

A single documentation artifact that serves two audiences simultaneously — human and AI — through structurally separated layers within the same document. Neither layer can be removed without breaking the artifact.

### How It Works

Every HUAN artifact carries two structurally distinct sections:

**Irreducible Concept** — Human-readable. Philosophy, meaning, narrative. The "why." Prose with examples. A founder or engineer reads this to understand what the artifact means.

**Irreducible Context** — AI-readable. Source paths, dependencies, versions, operational data. Structured fields. An AI role (Builder, Tester, Analyst) reads this to understand what the artifact requires to act.

Both sections live in the same file. The separation is structural (marked sections), not physical (separate files). One artifact, two audiences, zero duplication.

### Novelty

- **Prior art:** API documentation separates human prose from machine-readable schemas (OpenAPI, JSDoc). README files intermix human explanation with command examples. Wiki systems have talk pages separate from content pages. None of these enforce dual-audience as a structural invariant — the separation is conventional, not contractual.
- **HUAN innovation:** Dual-audience is the invariant. An artifact missing either layer is not HUAN-compliant. The invariant is enforceable by automated tooling (huan-analyst) and acts as a quality gate (huan-lifecycle). This is not a documentation convention — it is a format specification with computable compliance.

### Implementation Status

- **huan-spec v1.0.2** drafted (2026-05-15). Defines the atomic card format.
- **137 ZK cards** carry Irreducible Concept + Irreducible Context sections (appended 2026-05-13).
- **Zero concept-without-context, zero context-without-concept** verified across all cards.
- **22 hybrid cards** flagged for splitting — cards where concept and context are naturally entangled and need separation.

---

## Concept 2 — Bidirectional Edge Contract as Lifecycle Gate

### Summary

Visual artifacts are validated not by visual inspection of the rendered diagram, but by verifying that every edge in the diagram has a corresponding bidirectional reference in the card graph. The diagram is correct if and only if the underlying graph edges are bidirectional.

### How It Works

**mdwiki 2-way edge rule:** For a visual artifact (diagram) to pass the lifecycle gate:
1. Every edge rendered in the diagram must correspond to a card reference in the source card graph (A references B).
2. The referenced card must also reference back (B references A).
3. If either direction is missing, the diagram fails validation — regardless of how it looks.

The gate operates on the graph, not the visual. A human sees a diagram. An AI validates the edges. The visual artifact is a view of the graph; correctness is a graph property, not a visual one.

### Novelty

- **Prior art:** Diagram-as-code tools (Mermaid, PlantUML, D2) validate syntax, not semantics. A syntactically valid diagram can be semantically wrong — node A connects to node B but B has no relationship to A. Architecture diagrams in wikis and docs are validated by human review, not by graph analysis.
- **HUAN innovation:** Validation is a graph operation, not a visual inspection. The lifecycle gate is computable — automated CI can block a diagram from advancing to `huan` status if edge contracts are violated. The visual is a view; the graph is the truth.

### Implementation Status

- **huan-visual pillar planned.** Skill file only — no separate spec.
- **mdwiki 2-way edge rule** defined conceptually (2026-05-15). Formal definition deferred to huan-lifecycle spec.
- **No implementation yet.** Depends on huan-lifecycle (formal state machine) and huan-visual (skill file).

---

## Concept 3 — Card Graph → Visual Rendering Without Separate Diagram Language

### Summary

Diagrams are rendered directly from the card graph structure. No separate diagram language or syntax is required. The card graph IS the diagram source. Rendering is a view, not a separate artifact.

### How It Works

A HUAN-compliant card graph carries:
- **Nodes** — cards (ZK-001, ZK-042, etc.)
- **Edges** — cross-references (ZK-001 references ZK-042, typed by relationship)
- **Metadata** — status, tags, domain, creation date

A renderer (huan-visual) traverses the graph and produces a visual representation. The renderer is a view engine. The graph is the single source of truth. Changing a card reference updates the diagram automatically — no separate diagram file to keep in sync.

### Novelty

- **Prior art:** Architecture diagrams require a separate artifact (Mermaid file, D2 file, draw.io file, diagram embedded in markdown). Keeping the diagram in sync with the architecture requires manual discipline. Wiki pages with diagrams drift from the source code and architecture docs they describe.
- **HUAN innovation:** The diagram is not a separate artifact. It is a rendered view of the card graph. Coherence is automatic — if the card graph is coherent, the diagram is correct. If the diagram is wrong, the card graph has an edge problem, not a diagram problem.

### Implementation Status

- **huan-visual pillar planned.** The skill file defines the rendering process.
- **No rendering engine selected.** Candidates: Mermaid (subgraph from data), D2 (programmatic generation), custom.
- **Edge contract** (relationship types, direction, strength) not yet formalized.
- **Dependency:** huan-spec (card format defines graph structure) + huan-lifecycle (bidirectional edge gate).

---

## Concept 4 — Tension Detection as Computable Graph Property

### Summary

Coherence violations across a documentation corpus are detectable algorithmically by analyzing the card graph structure. Tension is not subjectively assessed — it is a computable property of the graph.

### How It Works

HUAN Analyst (pillar 7) scans the card graph for computable tension signals:

| Tension Type | Detection Method |
|---|---|
| Concept/context mismatch | Card claims `huan` status but concept and context sections are in semantic conflict (LLM-classified) |
| Stale references | Referenced file paths don't resolve on disk |
| Circular dependencies | A → B → A reference chains detected via graph traversal |
| Orphan cards | No inbound references from any other card |
| Duplicate concepts | Two cards with overlapping concept sections and no cross-reference |
| Version skew | Card A references card B v1, but card B is now v2 |

Each tension type has a computable detection algorithm. The report is structured (machine-readable) for downstream agentic remediation.

### Novelty

- **Prior art:** Documentation rot detection exists (broken links in wikis, stale README references). Linters check markdown syntax and link validity. Static analysis tools detect circular imports in code. None of these operate on a graph of documentation artifacts with semantic concept/context analysis.
- **HUAN innovation:** Tension detection is graph-native. The corpus is a graph (nodes = cards, edges = references). Coherence violations are graph anomalies. The analyst doesn't "read" documentation — it computes graph properties. This makes documentation quality a CI-gateable property.

### Implementation Status

- **huan-analyst pillar planned.** Depends on pillars 1-6 for detection surface.
- **Detection surface contract** not yet defined — what pillars 1-6 must expose for the analyst to query.
- **Tension taxonomy** drafted in pillar-roadmap (6 tension types). Formal taxonomy deferred to huan-analyst spec.
- **No implementation yet.** Large effort — full graph traversal + semantic analysis.

---

## Concept 5 — Seed-to-Pruned Lifecycle with Deprecation Propagation

### Summary

A formal state machine for documentation artifact lifecycle where pruning a card automatically propagates deprecation signals to all dependent cards, triggering status review or downgrade.

### How It Works

Cards progress through a defined state machine:

```
seed → growing → huan → pruned (dual-audience path)
```

Each transition is gated:
- **seed → growing:** Concept and context drafted. Steward review.
- **growing → huan:** Concept/context coherent. Cross-references present. Tension-free (analyst-verified). AI-referenceable.
- **growing → huan:** Coherent. All relates-to reciprocate. Tension-free. huan-compliant set by lifecycle gate.
- **Any → pruned:** Content migrated or obsolete. Deprecation reason documented.

**Prune propagation:** When card X is pruned:
1. All cards that reference X are flagged.
2. Flags are visible in INDEX and diagnostic logs.
3. Flagged cards are demoted from `huan` to `growing` until the reference is resolved.
4. Resolution paths: update reference to successor card, remove reference, or mark as "intentionally stale."
5. Propagation cascades — if card Y references X and card Z references Y, Z is also flagged.

### Novelty

- **Prior art:** Deprecation in software (deprecated API endpoints, @deprecated annotations, package versioning). Documentation versioning (git history, "last updated" dates). Wiki pages have "this page is outdated" banners added manually. None of these propagate deprecation automatically through a dependency graph.
- **HUAN innovation:** Deprecation is a graph operation. Pruning one node triggers automatic status review of all dependent nodes. The propagation is computable — automated tooling can flag, demote, and report without human scanning. This makes documentation maintenance a structured process, not a manual cleanup task.

### Implementation Status

- **huan-lifecycle pillar planned.** Formal spec with state machine definition.
- **State machine** defined conceptually (ZK-000 template, INDEX status legend, huan-card-structure prompt). Formalization is the work.
- **Transition gates** partially defined. Triggers (Steward review, Analyst scan, age-based) not yet formalized.
- **No implementation yet.** Small effort — one spec document. Formal state machine definition with transition tables.

---

## Submission Pipeline

```
1. Draft disclosure (this document)
2. Internal review (Advisor + founder)
3. Legal review (deferred per ZK-081 — legal entity not yet formed)
4. HPE submission (open-source office review)
5. Public release (GitHub: governorofentropy)
```

**Current stage:** Draft disclosure. Internal review pending.

## Licensing Intent

All HUAN artifacts (specs, skill files, examples) to be released under MIT license. The standard is open. Implementations may use any license.

---

## Supporting Artifacts

| Artifact | Path | Status |
|----------|------|--------|
| FL-003 product definition | `docs/flight-level/FL-003-huan.md` | Created 2026-05-15 |
| HUAN PM skill file | `skills/huan-pm/SKILL.md` | Created 2026-05-15 |
| Pillar roadmap | `docs/huan-standard/pillar-roadmap.md` | Created 2026-05-15 |
| Coherence audit | `docs/audit/coherence-audit-2026-05-15.md` | Created 2026-05-15 |
| huan-spec (draft) | TBD | Drafted 2026-05-15, not yet written to disk |
| huan-skill (draft) | `skills/huan-pm/SKILL.md` | This is the skill file |

---

## Open Questions

1. **Legal entity:** HPE submission requires an entity. ZK-081 defers legal entity formation. Interim: submit as individual (founder) with entity assignment upon formation?
2. **Prior art search:** Has any formal prior art search been conducted for these 5 concepts? Advisor session did not reference one.
3. **Provisional patents:** Should provisional applications be filed before open-source disclosure? Standard practice is file-then-disclose.
4. **HPE process:** What is the actual HPE open-source submission process? Contact? Form? Review timeline?

---

*Lv25:10*
