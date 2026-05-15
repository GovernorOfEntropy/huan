# HUAN Pillar Roadmap

**Status:** Phase B complete — 4 pillars drafted (2026-05-15)
**Owner:** HUAN PM (FL-022)
**Two pillars drafted:** huan-spec ✅, huan-skill ✅
**Four pillars drafted:** huan-lifecycle ✅, huan-h2r ✅, huan-diagnostic ✅, huan-visual ✅
**Two pillars planned:** huan-analyst, huan-agent

---

## Build Order

```
Phase A (foundation):  huan-spec ✅ + huan-skill ✅
Phase B (independent): huan-lifecycle ✅, huan-h2r ✅, huan-diagnostic ✅, huan-visual ✅
Phase C (complete):    huan-analyst — tension detection, 6-type taxonomy
Phase D (complete):    huan-surgeon — agentic remediation, auto-fix/propose/escalate
```

Phase B complete — all 4 pillars drafted in parallel (2026-05-15). Phase C unblocked.

---

## Pillar 3: huan-lifecycle

**Type:** Format (spec)
**Status:** Drafted (v1.0.0)
**Key ZK Cards:** ZK-139, ZK-140, ZK-141
**Output:** `docs/huan-standard/huan-lifecycle-1.0.0.md` (9,275 chars)

Formal state machine: seed→growing→huan→pruned (dual-audience) + seed→growing→evergreen→pruned (machine-consumed). Transition gates, prune propagation, bulk operations, mdwiki 2-way edge rule.

---

## Pillar 4: huan-h2r

**Type:** Process (skill file)
**Status:** Drafted (v1.0.0)
**Key ZK Cards:** ZK-111, ZK-004, ZK-073
**Output:** `docs/huan-standard/huan-h2r-1.0.0.md` (9,513 chars)

Human-to-Role retrieval pipeline. Query decomposition, graph traversal, relevance scoring, role-aware filtering, token budget enforcement, fallback chain.

---

## Pillar 5: huan-diagnostic

**Type:** Format (spec)
**Status:** Drafted (v1.0.0)
**Key ZK Cards:** ZK-072, ZK-098, ZK-046
**Output:** `docs/huan-standard/huan-diagnostic-1.0.0.md` (9,024 chars)

Card health diagnostic format. NDJSON events, 8 diagnostic dimensions, severity taxonomy, scan cadence, consumer contracts.

---

## Pillar 6: huan-visual

**Type:** Process (skill file)
**Status:** Drafted (v1.0.0)
**Key ZK Cards:** ZK-039, ZK-054, ZK-095
**Output:** `docs/huan-standard/huan-visual-1.0.0.md` (10,613 chars)

Card graph → visual diagram. Dual-audience rendering, mdwiki 2-way edge rule enforcement, edge contract, annotation separation, theme-aware renders.

---

## Pillar 7: huan-analyst

**Type:** Process (skill file)
**Status:** Planned
**Dependencies:** huan-spec, huan-lifecycle, huan-diagnostic (needs detection surface from pillars 1-6)

### What It Defines

Tension detection as a computable graph property. HUAN Analyst scans the card graph for coherence violations: concept/context mismatch, stale references, circular dependencies, orphan cards, duplicate concepts, version skew.

### Key Design Decisions

1. Scan model — full graph traversal, incremental, or hybrid?
2. Severity taxonomy — what's a warning vs. what blocks huan status?
3. Report format — structured + prose?
4. Auto-remediation — report-only or fix simple problems?
5. Cadence — on-change, scheduled, or both?
6. Detection surface — what pillars 1-6 expose that the analyst can query

### Artifacts

- `huan-analyst-1.0.0.md` — skill file (process definition)
- Tension taxonomy
- Report format spec
- Detection surface contract

### Estimated Effort

Large. Needs all 6 prior pillars to define the detection surface.

---

## Pillar 8: huan-agent

**Type:** Process (skill file)
**Status:** Planned
**Dependencies:** huan-analyst (needs analyst output contract)

### What It Defines

Closes the loop after analyst. Agentic remediation: auto-fix, propose, escalate, verify.

### Key Design Decisions

1. Autonomy level — fully automatic, human-in-the-loop, or advisory?
2. Remediation scope — card-level only, or INDEX, cross-references, skill files?
3. Safety gates — what can the agent NEVER do?
4. Audit trail — every action logged with before/after and rollback path
5. Escalation chain — agent → HUAN PM → PM-PM → founder

### Artifacts

- `huan-agent-1.0.0.md` — skill file (process definition)
- Remediation action taxonomy
- Safety gate specification
- Audit trail format

### Estimated Effort

Medium. Depends entirely on analyst output contract.

---

## Summary

| Pillar | Type | Effort | Status | Blocks | Blocked By |
|--------|------|--------|--------|--------|------------|
| huan-spec | Format | — | Drafted v1.0.1 | — | — |
| huan-skill | Process | — | Drafted v1.0.1 | — | — |
| huan-lifecycle | Format | Small | Drafted v1.0.0 | — | huan-spec |
| huan-h2r | Process | Medium | Drafted v1.0.0 | — | huan-spec |
| huan-diagnostic | Format | Small | Drafted v1.0.0 | — | huan-spec, lifecycle |
| huan-visual | Process | Medium | Drafted v1.0.0 | — | huan-spec, lifecycle |
| huan-analyst | Process | Large | Planned | agent | pillars 1-6 |
| huan-agent | Process | Medium | Planned | — | analyst |

**Next action:** HUAN PM transitions to Phase C — draft huan-analyst once detection surface is verified across pillars 1-6.

---

*Lv25:10*
