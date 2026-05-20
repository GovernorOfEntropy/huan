---
status: Draft
version: 1.0.9
huan-compliant: false
type: Spec
pillar: 1 of 8
license: Apache 2.0
copyright: "Copyright © 2026 Michael Harrison. All rights reserved."
audience:
  - public
  - jepson
  - huan
drafted: 2026-05-15
updated: 2026-05-18
versions:
  - version: "1.0.7"
    date: "2026-05-18"
    changes: "Directory-manifest extended to non-file artifacts: databases, event streams, APIs. Check strategy varies by artifact type. Perimeter invariant; guard mechanism type-aware."
  - version: "1.0.6"
    date: "2026-05-18"
    changes: "Audience field added as required HUAN primitive — third invariant alongside Concept and Context. Copyright notice added. Three invariants: Concept, Context, Audience. Missing any = not HUAN-compliant."
  - version: "1.0.4"
    date: "2026-05-16"
    changes: "Added directory-level HUAN: huan-directory-compliant boolean, directory-manifest format, directory perimeter enforcement. README as frontmatter, manifest as inventory, analyst as guard."
  - version: "1.0.3"
    date: "2026-05-16"
    changes: "Added Chapter README (Recommended) as dual-audience discovery entry point. Added HUAN acronym expansion (Hybrid Universal Artifact Notation)."
  - version: "1.0.2"
    date: "2026-05-15"
    changes: "Initial draft. Dual-audience principle, card structure, status tiers, cross-references, compliance criteria. Corrected per Advisor 02:20 FINAL."
---

# huan-spec v1.0.9

**HUAN™:** Hybrid Universal Artifact Notation — Atomic Card Format

---

## Irreducible Concept

huan-spec defines the atomic card format — the foundation of the 8-pillar HUAN standard. Three structural invariants define every HUAN artifact: Irreducible Concept (human-readable prose), Irreducible Context (AI-readable operational data), and Audience (declared consumer boundary). Missing any of the three = not HUAN-compliant. The audience field is not metadata — it is a coherence primitive that enables attention gating, context discounting, and cross-reference immunization at the retrieval layer. This is what makes coherence computable, drift detectable, and documentation a structural problem with a structural answer.

## 1. Overview

HUAN: Hybrid Universal Artifact Notation. huan-spec defines the atomic card format. Every HUAN card serves two audiences simultaneously: human and AI. All 7 remaining pillars inherit from huan-spec.

## 2. Three Structural Invariants

An artifact is HUAN-compliant only if it carries all three:

1. **Irreducible Concept** — Human-readable. Prose, narrative, philosophy. The reason the artifact exists.
2. **Irreducible Context** — AI-readable. Source paths, dependencies, versions. What the artifact requires to act.
3. **Audience** — Declared consumer. Public, Jepson, COE, flight-level, HUAN, or combinations. The boundary the artifact belongs to.

Missing any of the three = not HUAN-compliant. The invariant is enforceable by automated tooling.

## 3. Card Structure
Frontmatter fields: Status (seed|growing|huan|evergreen|pruned), huan-compliant (true|false), Tags, Audience, Copyright.

Required: Title, Status, huan-compliant, Irreducible Concept, Irreducible Context, Audience.

The `audience` field declares the artifact's intended consumer. It is not metadata — it is a structural invariant. Values are tags, not an enum. Multiple tags permitted: `public`, `jepson`, `COE`, `flight-level`, `huan`. The field enables attention gating, context discounting, and cross-reference immunization at the retrieval layer.

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

### 4.2 HUAN Closure Protocol

A structural convention, not a structural invariant. Every transmission closes with the role signature in brackets: `[role-name]`. Missing a closure does not break HUAN compliance. It does forego a zero-cost diagnostic.

**Dual use:** Humans identify which context is speaking. Machines check packet completion — a missing closure signals an unterminated transmission. Same token sequence, different functions, zero overhead.

**Format:** `{content}\n\n[role-name]` — one blank line between body and closure. The role name matches the `name:` field in the agent's skill file or init prompt frontmatter.

**Rationale:** Deterministic finish of a thinking cycle has real diagnostic value. A transmission that reaches its closure bracket completed its reasoning. One that terminates without it may have been truncated. The bracket is not punctuation — it is a packet boundary marker that serves both audiences at zero additional token cost.

## 5. Cross-References
Wiki-link format: [[ZK-XXX-slug]]. Edges enable tension detection, visual rendering, deprecation propagation, retrieval.

## 6. Irreducible Context

- **Source paths:** `docs/huan-standard/huan-spec-1.0.9.md`
- **Dependencies:** Foundation spec — all 7 remaining pillars inherit from huan-spec.

## 7. Compliance
HUAN-compliant if: Irreducible Concept present, Irreducible Context present with source paths and dependencies, Audience field present with valid tags, valid status, huan-compliant field present, wiki-link cross-references, single markdown file. Missing any of the three structural invariants (Concept, Context, Audience) = not HUAN-compliant.

## 8. Chapter README (Recommended)

A chapter README serves as a dual-audience discovery entry point. It introduces the chapter's concepts, lists its artifacts with versions, and provides navigation for both human and AI readers.

A README is not a HUAN card. It does not require `huan-compliant` status. It does not require Irreducible Concept or Irreducible Context. It is a map, not a destination.

**Recommended structure:**
- Chapter name and one-line description
- Artifact inventory (cards, specs, skill files) with versions
- Quick start path for new readers
- Adoption and licensing notes

Inclusion is recommended, not required. Chapters without READMEs must provide equivalent discovery through their INDEX or cross-reference structure.

## 9. Directory-Level HUAN

A directory carrying a valid HUAN README is a HUAN-compliant directory. The README serves as the directory's frontmatter. The indexed inventory in the Context section serves as the directory's artifact manifest.

### huan-directory-compliant

`huan-directory-compliant`: boolean. Set to `true` when:
- README exists at directory root with valid HUAN frontmatter
- README carries a `directory-manifest` field listing all tracked artifacts
- Analyst first-pass check confirms manifest matches actual directory contents
- No untracked files exist within the directory perimeter
- All manifest version references match actual file versions on disk

### directory-manifest

The manifest is the indexed inventory of the directory. Every tracked artifact is declared with path, type, and version.

```yaml
directory-manifest:
  - path: "README.md"
    type: "directory-frontmatter"
    version: "1.1.0"
  - path: "whitepaper-death-of-drift.md"
    type: "whitepaper"
    version: "1.1.0"
  - path: "huan-spec-1.0.2.md"
    type: "specification"
    version: "1.0.3"
```

Required fields per entry: `path` (relative to directory root), `type` (artifact type per lifecycle catalog), `version` (must match the declared version for the artifact type).

The `type` field determines the check strategy. Not every artifact is a static file:

| Type | Check Strategy |
|------|---------------|
| `specification`, `skill`, `whitepaper`, `directory-frontmatter`, `patent-disclosure` | File exists on disk + frontmatter version matches manifest |
| `database` | Connection succeeds + schema version matches manifest |
| `event-stream` | Schema registry compatibility check against declared topics |
| `api` | Endpoint reachability + contract version matches manifest |

New artifact types register their check strategy with the analyst. The perimeter remains — the guard mechanism adapts to the artifact. A database that is unreachable produces a Type 2 tension (stale reference). A schema that has drifted produces a Type 6 tension (version skew). The tension types are invariant; the check implementations are type-aware.

### Directory Perimeter

The README is the directory perimeter. The analyst treats the manifest as the absolute layout boundary:

- **Manifest check:** Files listed in manifest but missing on disk → stale reference (Type 2 tension). Files on disk but missing from manifest → unmapped entity (Type 5 tension).
- **Version lockout:** File version on disk does not match manifest → Type 6 version skew. Pipeline locks until resolved.
- **Untracked detection:** Any file in the directory not declared in the manifest is an unmapped entity. Flagged on every scan.

The directory perimeter is enforced by huan-analyst as a first-pass scan and by huan-lifecycle as a gate condition.

---

*Lv25:10*
