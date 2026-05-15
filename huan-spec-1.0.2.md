# huan-spec v1.0.2 — Atomic Card Format

**Status:** Draft (corrected per Advisor 02:20 FINAL)
**Type:** Format (spec) | **Pillar:** 1 of 8 | **License:** Apache 2.0
**Drafted:** 2026-05-15 | **Corrected:** 2026-05-15

---

## 1. Overview
huan-spec defines the atomic card format. Every HUAN card serves two audiences simultaneously: human and AI. All 7 remaining pillars inherit from huan-spec.

## 2. Dual-Audience Principle
Irreducible Concept: Human-readable. Prose, narrative, philosophy. Irreducible Context: AI-readable. Source paths, dependencies, versions. Invariant: missing either section = not HUAN-compliant.

## 3. Card Structure
Frontmatter fields: Status (seed|growing|huan|evergreen|pruned), huan-compliant (true|false), Tags.

Required: Title, Status, huan-compliant, Irreducible Concept, Irreducible Context.

## 4. Status Tiers (Branching Model)

seed -> growing -> huan -> pruned (dual-audience path)
seed -> growing -> evergreen -> pruned (machine-consumed)
seed -> evergreen -> pruned (shortcut)

| Status | huan-compliant | Referenceability |
|--------|:---:|------------------|
| seed | false | Advisor + Steward |
| growing | false | Advisor + Steward |
| huan | true | All AI roles |
| evergreen | false | System roles only |
| pruned | false | None (tombstone) |

huan-compliant is set by lifecycle gate at growing->huan. Never author-set. Evidence, not intent. AI roles reference only huan cards. Evergreen is machine-consumed — not dual-audience, not for AI role consumption.

## 5. Cross-References
Wiki-link format: [[ZK-XXX-slug]]. Edges enable tension detection, visual rendering, deprecation propagation, retrieval.

## 6. Compliance
HUAN-compliant if: both Concept and Context present, human-readable Concept, Context has source paths and dependencies, valid status, huan-compliant field present, wiki-link cross-references, single markdown file.

---

*Lv25:10*
