# HUAN Standard — Changelog

Tracks why the standard evolved, what real-world friction exposed each gap, which pillar revision addressed it, and cross-pillar dependencies changed together.

---

## v1.0.2 (2026-05-16)

**Trigger:** Whitepaper had no valid lifecycle state.

**What happened:** The whitepaper ("Death of Drift") was written but could not be placed in the lifecycle. The existing model assumed every document is on the HUAN-compliance arc. Whitepapers are not — they are persuasive artifacts with their own lifecycle needs. This gap did not surface in design review; it surfaced when a real artifact had nowhere to live.

**Resolution:**
- huan-lifecycle v1.0.2: added Extensibility section. Custom arcs for non-HUAN document types (whitepaper, HPE submission, journal).
- Added two new lifecycle states: noodle (raw capture, pre-seed) and draft (structured, not corpus-ready).
- ZK-152: Failure as Signal — the gap was the system self-diagnosing.

**Affected:** huan-lifecycle, whitepaper, Advisor workflow, HPE submission package.

---

## v1.0.1 (2026-05-15)

**Trigger:** Evergreen state ambiguity.

**What happened:** Advisor and founder cycled through three lifecycle corrections in one session. The original linear model (seed→growing→huan→evergreen→pruned) collapsed when evergreen was redefined as machine-consumed, not a stable HUAN card.

**Resolution:** Branching state model. Dual-audience path (seed→growing→HUAN→pruned) and machine-consumed path (seed→growing→evergreen→pruned). Added huan-compliant boolean field, set by lifecycle gate.

**Affected:** All 8 pillars.

---

*Lv25:10*
