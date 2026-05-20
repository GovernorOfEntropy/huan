---
status: huan
version: 1.1.3
huan-compliant: false
huan-directory-compliant: false
type: directory-frontmatter
license: Apache 2.0
copyright: "Copyright © 2026 Michael Harrison. All rights reserved."
audience:
  - public
  - huan
  - COE
drafted: 2026-05-15
updated: 2026-05-19
directory-manifest:
  - path: "README.md"
    type: "directory-frontmatter"
    version: "1.1.2"
  - path: "whitepaper-death-of-drift.md"
    type: "whitepaper"
    version: "1.3.0"
  - path: "huan-spec-1.0.9.md"
    type: "specification"
    version: "1.0.9"
  - path: "huan-lifecycle-1.1.2.md"
    type: "specification"
    version: "1.1.2"
  - path: "huan-h2r-1.1.0.md"
    type: "skill"
    version: "1.1.0"
  - path: "huan-diagnostic-1.0.1.md"
    type: "specification"
    version: "1.0.1"
  - path: "huan-visual-1.0.1.md"
    type: "skill"
    version: "1.0.1"
  - path: "huan-analyst-1.2.2.md"
    type: "skill"
    version: "1.2.2"
  - path: "huan-surgeon-1.2.3.md"
    type: "skill"
    version: "1.2.3"
versions:
  - version: "1.1.3"
    date: "2026-05-19"
    changes: "Surgeon pass 2 — cascade remediation complete. Manifest paths corrected to match disk: huan-spec-1.0.9.md, huan-lifecycle-1.1.2.md, huan-analyst-1.2.2.md, huan-surgeon-1.2.3.md. Manifest versions aligned. README Irreducible Context source paths and parenthetical versions fixed. Body headings synced on lifecycle, analyst, surgeon. Cross-card version references bumped in patent-concepts and whitepaper. huan-directory-compliant set to false pending analyst re-scan clearance."
  - version: "1.1.2"
    date: "2026-05-19"
    changes: "Manifest filenames and versions synchronized with disk after surgeon pass. huan-spec v1.0.9, analyst v1.2.1, lifecycle v1.1.1, h2r v1.1.0, surgeon v1.2.0"
  - version: "1.1.1"
    date: "2026-05-19"
    changes: "Updated manifest for patent-concepts.md, huan-spec v1.0.8, huan-analyst v1.2.1. Lifecycle version bump."
  - version: "1.1.0"
    date: "2026-05-16"
    changes: "Added directory-manifest and HUAN-compliant frontmatter. All 8 pillars + whitepaper declared with current versions."
  - version: "1.0.0"
    date: "2026-05-15"
    changes: "Initial README. 8-pillar overview, quick start, adoption notes."
---

# HUAN™ Standard

**HUAN:** Hybrid Universal Artifact Notation
**License:** Apache 2.0
**Repository:** github.com/governorofentropy/huan-standard

---

## Irreducible Concept

HUAN is an open standard for dual-audience documentation. Every artifact serves humans and AI simultaneously — one file, two readers, zero translation. The standard defines I/O contracts at the seams. Implementations compete on what happens inside.

This directory is the canonical registry of the HUAN standard. It contains the 8-pillar architecture — the atomic card format, the lifecycle state machine, the retrieval pipeline, the diagnostic layer, the visual renderer, the tension analyst, and the remediation surgeon. Every artifact is versioned. Every version is declared.

**This README is the directory perimeter.** It carries a `directory-manifest` — the indexed inventory of every artifact. The manifest is the source of truth. The analyst compares it against disk on every scan. A file listed but missing is a stale reference. A file on disk but not in the manifest is an unmapped entity. A version mismatch locks the pipeline. This directory knows its own contents, enforces its own version boundaries, and computes its own structural health through this single file. This turns a file folder into an object-oriented database primitive.

## Irreducible Context

- **Source paths:** `docs/huan-standard/huan-spec-1.0.9.md` (v1.0.9), `docs/huan-standard/huan-lifecycle-1.1.2.md` (v1.1.2), `docs/huan-standard/huan-h2r-1.1.0.md` (v1.1.0), `docs/huan-standard/huan-diagnostic-1.0.1.md` (v1.0.1), `docs/huan-standard/huan-visual-1.0.1.md` (v1.0.1), `docs/huan-standard/huan-analyst-1.2.2.md` (v1.2.2), `docs/huan-standard/huan-surgeon-1.2.3.md` (v1.2.3), `docs/huan-standard/whitepaper-death-of-drift.md` (v1.3.0)
- **Dependencies:** huan-spec v1.0.9 (atomic card format, core standard inherited by all pillars)
- **Directory perimeter:** manifest-to-disk match enforced by huan-analyst v1.2.2. Version lockout enforced by huan-lifecycle v1.1.2.
- **Implementation:** Reference runtime available. Any conforming implementation is valid.

## The 8 Pillars

| # | Pillar | Type | Description |
|---|--------|------|-------------|
| 1 | huan-spec | Format | Atomic card format. Foundation. |
| 2 | huan-skill | Process | Tech Writer PM. To be released.
| 3 | huan-lifecycle | Format | State machine: seed → growing → HUAN → pruned. |
| 4 | huan-h2r | Process | Human-to-Role retrieval pipeline. |
| 5 | huan-diagnostic | Format | Card health monitoring. |
| 6 | huan-visual | Process | Card graph → diagram rendering. |
| 7 | huan-analyst | Process | Tension detection across the corpus. |
| 8 | huan-surgeon | Process | Agentic remediation. Closes the loop. |

## Quick Start

1. Read huan-spec v1.0.9 — the atomic card format
2. Write a card with Irreducible Concept + Irreducible Context
3. Apply a status: seed, growing, or huan
4. Cross-reference related cards with [[wiki-links]]
5. *Suggested:* Append a trailing `[your-role-name]` HUAN Closure to the file terminus as a zero-semantic tax parity bit for automated runtime validation.

## Adoption

HUAN defines I/O contracts. Implementations compete on quality. The reference runtime is not required. Any tool that reads and writes HUAN-compliant cards is a valid HUAN implementation.

## Source Thesis & Alignment

The foundational engineering theory behind the HUAN standard is documented and updated live on Substack. Before implementing the serialization contracts in this repository, review the core framework design:


For technical implementation details, inherit the core specification directly:
1. Review `huan-spec-1.0.9.md` for the atomic card format foundation.
2. Track corpus state transitions via `huan-lifecycle-1.1.2.md`.

## License

Apache 2.0. See LICENSE.

---

*Lv25:10*
