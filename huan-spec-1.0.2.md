---
status: Draft
version: 1.0.4
huan-compliant: false
type: Spec
pillar: 1 of 8
license: Apache 2.0
drafted: 2026-05-15
updated: 2026-05-16
versions:
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

# huan-spec v1.0.2

**HUAN:** Hybrid Universal Artifact Notation — Atomic Card Format

---

## 1. Overview

HUAN: Hybrid Universal Artifact Notation. huan-spec defines the atomic card format. Every HUAN card serves two audiences simultaneously: human and AI. All 7 remaining pillars inherit from huan-spec.

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

## 7. Chapter README (Recommended)

A chapter README serves as a dual-audience discovery entry point. It introduces the chapter's concepts, lists its artifacts with versions, and provides navigation for both human and AI readers.

A README is not a HUAN card. It does not require `huan-compliant` status. It does not require Irreducible Concept or Irreducible Context. It is a map, not a destination.

**Recommended structure:**
- Chapter name and one-line description
- Artifact inventory (cards, specs, skill files) with versions
- Quick start path for new readers
- Adoption and licensing notes

Inclusion is recommended, not required. Chapters without READMEs must provide equivalent discovery through their INDEX or cross-reference structure.

## 8. Directory-Level HUAN

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

Required fields per entry: `path` (relative to directory root), `type` (artifact type per lifecycle catalog), `version` (must match the file's declared version).

### Directory Perimeter

The README is the directory perimeter. The analyst treats the manifest as the absolute layout boundary:

- **Manifest check:** Files listed in manifest but missing on disk → stale reference (Type 2 tension). Files on disk but missing from manifest → unmapped entity (Type 5 tension).
- **Version lockout:** File version on disk does not match manifest → Type 6 version skew. Pipeline locks until resolved.
- **Untracked detection:** Any file in the directory not declared in the manifest is an unmapped entity. Flagged on every scan.

The directory perimeter is enforced by huan-analyst as a first-pass scan and by huan-lifecycle as a gate condition.

---

*Lv25:10*
