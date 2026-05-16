---
status: Draft
version: 1.0.4
huan-compliant: false
type: Spec
pillar: 3 of 8
license: Apache 2.0
drafted: 2026-05-15
updated: 2026-05-16
versions:
  - version: "1.0.3"
    date: "2026-05-16"
    changes: "Added directory perimeter gate — manifest-to-disk match required for chapter compliance. Version lockout on manifest skew. Referenced huan-spec v1.0.4 and huan-analyst v1.1.0."
  - version: "1.0.2"
    date: "2026-05-15"
    changes: "Initial draft. State machine, transitions, prune propagation, 2-way edge rule. Corrected per Advisor 02:20 FINAL."
---

# huan-lifecycle v1.0.2 — corrected per Advisor 02:20 FINAL

## Irreducible Concept

huan-lifecycle governs the state of every HUAN artifact. Cards progress through a branching state machine: seed → growing → huan → pruned. Every transition is gated. The mdwiki 2-way edge rule blocks promotion unless cross-references reciprocate. Deprecation propagates automatically — prune a card and every dependent is flagged within three hops. The directory perimeter gate extends this to the filesystem: a directory is not compliant unless its README manifest matches disk. The lifecycle is the structural defense against drift.

## 1. Scope
This lifecycle governs HUAN cards only. A HUAN card is always dual-audience. Non-HUAN artifacts (evergreen, raw logs, internal) exist alongside but are not governed by this lifecycle.

## 2. State Machine (Branching)
seed -> growing -> HUAN -> pruned (dual-audience path)
seed -> growing -> evergreen -> pruned (machine-only)
seed -> evergreen -> pruned (shortcut)

huan-compliant field: HUAN=true, all others=false. Set by lifecycle gate, not author.

## 3. Transitions
seed->growing: human-gated, concept+context primitives
growing->HUAN: hybrid-gated, coherence, 2-way edge rule
growing->evergreen: human-gated, classified machine-consumed
->pruned: always human-gated

## 4. Prune Propagation
Dependents flagged, up to 3 hops. Notification, not demotion.

## 5. 2-Way Edge Rule
HUAN cards must have bidirectional references. Foundational cards exempt.

## 6. Directory Perimeter Gate

A directory is not HUAN-compliant unless its README's `directory-manifest` passes the analyst first-pass check. The gate conditions:

- README exists at directory root with valid HUAN frontmatter
- `directory-manifest` field present and populated
- Manifest-to-disk match verified (analyst first-pass)
- Zero unmapped entities within the directory perimeter
- All manifest version references match actual file versions

Failure blocks all artifact lifecycle transitions within the directory. A chapter cannot advance cards while the directory perimeter is breached.

## 7. Version Lockout

When the analyst detects a manifest-to-disk version mismatch (Type 6 — Version Skew), the pipeline locks. No artifacts in the affected directory may advance status. The lock persists until:
- The manifest is updated to match file versions, or
- File versions are corrected to match the manifest

Lockout is per-directory. A breach in one chapter directory does not affect others.

## 8. Context
Source: huan-spec v1.0.4, huan-analyst v1.1.0
Implementation: Jepson Factory

---
*Lv25:10*
