---
status: Draft
version: 1.0.2
huan-compliant: false
type: Spec
pillar: 3 of 8
license: Apache 2.0
drafted: 2026-05-15
updated: 2026-05-15
versions:
  - version: "1.0.2"
    date: "2026-05-15"
    changes: "Initial draft. State machine, transitions, prune propagation, 2-way edge rule. Corrected per Advisor 02:20 FINAL."
---

# huan-lifecycle v1.0.2 — corrected per Advisor 02:20 FINAL

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

## 6. Context
Source: ZK-139/140/141, huan-spec v1.0.2
Implementation: Jepson Factory

---
*Lv25:10*
