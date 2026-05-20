---
status: Draft
version: 1.0.1
huan-compliant: false
type: Spec
pillar: 5 of 8
license: Apache 2.0
copyright: "Copyright © 2026 Michael Harrison. All rights reserved."
audience:
  - public
  - jepson
  - huan
drafted: 2026-05-15
versions:
  - version: "1.0.0"
    date: "2026-05-15"
    changes: "Initial draft. NDJSON event format, 8 diagnostic dimensions, severity taxonomy, scan cadence, consumer contracts."
---

# huan-diagnostic v1.0.1 — Card Health Diagnostic Format

---

## Irreducible Concept

huan-diagnostic defines the log format for card health monitoring — the detection surface the analyst queries. Every HUAN corpus produces diagnostic events: staleness alerts, broken paths, tension detections, orphan flags. These events are NDJSON-structured, severity-tagged, and carry remediation hints. Eight dimensions of card health are monitored. The diagnostic layer is the immune system's early warning — it detects decay before it becomes corruption.

## 1. Overview

huan-diagnostic defines the log format for card health monitoring. Every HUAN corpus produces diagnostic events — staleness alerts, broken paths, tension detections, orphan flags. This spec defines what those events look like, how they are structured, who consumes them, and what they mean.

Diagnostics are the immune system of a HUAN corpus. They detect decay before it becomes corruption. They surface problems while they are small. They provide the detection surface that huan-analyst queries and huan-agent remediates.

This spec inherits the dual-audience principle from huan-spec v1.0.9. Every diagnostic event serves both the human reader (what is wrong and why it matters) and the AI consumer (structured data for automated scanning).

## 2. Diagnostic Event Format

Every diagnostic event is a single line of structured output. The format is line-oriented JSON — one JSON object per line, newline-delimited (NDJSON). This enables streaming consumption, log aggregation, and grep-friendly debugging.

### Event Schema

```json
{
  "timestamp": "2026-05-15T14:30:00Z",
  "event_id": "diag-8a3f2b1c",
  "severity": "warning",
  "card": "ZK-111",
  "dimension": "staleness",
  "message": "Card ZK-111 has not been modified in 45 days. Expected refresh cadence: 30 days.",
  "details": {
    "last_modified": "2026-03-31T10:00:00Z",
    "days_stale": 45,
    "refresh_cadence_days": 30,
    "status": "huan",
    "dependency_count": 12
  },
  "remediation_hint": "Review card for staleness. Consider updating or graduating to huan."
}
```

### Required Fields

| Field | Type | Description |
|-------|------|-------------|
| timestamp | ISO 8601 | When the diagnostic event was generated |
| event_id | string | Unique identifier for this event |
| severity | enum | One of: info, warning, error, critical |
| card | string | The card identifier (ZK number) |
| dimension | enum | The diagnostic dimension (see §3) |
| message | string | Human-readable description of the finding |
| details | object | Structured data specific to the dimension |
| remediation_hint | string | Suggested action for the Steward or huan-agent |

## 3. Diagnostic Dimensions

### staleness

A card has not been modified within its expected refresh cadence.

**Severity:** warning → error (escalates with age)
**Details:** last_modified, days_stale, refresh_cadence_days, status, dependency_count
**Cadence defaults:** seed: 14 days, growing: 30 days, huan: 60 days, huan: 60 days

### path_rot

A referenced file path does not resolve. The file has been moved, renamed, or deleted.

**Severity:** error
**Details:** broken_path, referenced_in (which field), last_validated, expected_location
**Remediation:** Update the path to the new location, or mark the reference as historical.

### tension

A coherence violation between Concept and Context sections. The card claims a status or property that its content does not support.

**Severity:** error → critical (if card is at huan)
**Details:** tension_type (concept_context_mismatch, stale_dependency, version_skew), detected_by, detection_method, affected_fields
**Remediation:** Resolve the tension — update the card, split the card, or demote the status.

### orphan

A card has no inbound references from any other card in the corpus.

**Severity:** info → warning (escalates with time orphaned)
**Details:** days_orphaned, outbound_references, status, created_date
**Note:** Not all orphans are problems. Foundational cards are often referenced by many but no card explicitly says "I depend on ZK-001." Orphan detection should weight by card type — a spec card with no references is more concerning than a journal entry.

### circular_dependency

A reference chain forms a cycle: A → B → A, or longer A → B → C → A.

**Severity:** error → critical (if any card in the cycle is at huan)
**Details:** cycle_path (ordered list of card identifiers), cycle_length, detected_at
**Remediation:** Break the cycle. One reference in the chain is spurious or should be a "related" tag rather than a dependency.

### version_skew

A card references a version of a dependency that is no longer current.

**Severity:** warning → error (if the referenced version has been pruned)
**Details:** referenced_version, current_version, dependency_card, version_delta
**Remediation:** Update the version reference, or document why the old version is still correct.

### broken_cross_reference

A wiki-link resolves to a card that does not exist or has been pruned.

**Severity:** error
**Details:** broken_link, referenced_card, link_location (which section), pruned_to (if the card was pruned and has a successor)
**Remediation:** Update the link to the successor card, or remove the reference if no successor exists.

### coherence_drift

A card at huan has developed a tension with a card it references that was recently updated. This may indicate a dependency change that requires the huan card to be re-validated.

**Severity:** warning
**Details:** drifted_with (card ID), drift_type, detected_after_update_of, last_coherence_check
**Remediation:** Review both cards. Update the evergreen card, or flag it for review.

## 4. Severity Taxonomy

| Severity | Meaning | Action Required | Escalation |
|----------|---------|----------------|------------|
| info | Noteworthy but not actionable | None | None |
| warning | Should be addressed soon | Steward review within refresh cadence | Escalates to error if unaddressed for 2× cadence |
| error | Must be addressed | Steward action required | Blocks growing → huan transition for affected card |
| critical | Immediate action required | Steward action + notification | Blocks all references to affected card; may trigger auto-demotion |

## 5. Scan Cadence

Diagnostic scans run on a configurable cadence:

- **On-change:** When a card is modified, a targeted scan runs on that card and its immediate dependents (1-hop).
- **Daily:** Full-corpus scan for staleness, path_rot, orphan detection, and version_skew. Runs during low-activity windows.
- **Weekly:** Deep scan for circular_dependency, coherence_drift, and tension. Includes full dependency graph traversal.
- **On-demand:** Steward or Analyst may trigger a full scan at any time.

On-change scans are fast and targeted. Daily scans are comprehensive. Weekly scans are deep. The combination ensures problems are detected at the right granularity without overwhelming the system.

## 6. Consumers

| Consumer | What It Reads | What It Does |
|----------|--------------|--------------|
| Steward | All events | Reviews warnings and errors. Initiates remediation. |
| huan-analyst | warning, error, critical events | Aggregates into tension reports. Detects patterns across cards. |
| huan-agent | error, critical events with remediation_hint | Attempts automated fixes for deterministic problems (path_rot, version_skew). |
| HUAN PM | Aggregated metrics | Tracks corpus health over time. Identifies systemic issues. |
| Jepson Factory | error, critical events | Blocks builds that depend on affected cards. |

## 7. Output Destinations

Diagnostic events are written to:

1. **Diagnostic log file:** `diagnostic.log` in the corpus root. Append-only. Rotated weekly.
2. **Diagnostic stream:** Real-time event stream for live consumers (huan-analyst, Jepson build gates).
3. **INDEX:** A summary of the most recent scan (last scan timestamp, event counts by severity, cards with open issues).

The log file is the durable record. The stream is for real-time consumers. The INDEX is for quick status checks.

## 8. Compliance

A diagnostic implementation is HUAN-compliant if:
1. Events are emitted in NDJSON format per the schema in §2
2. All 8 diagnostic dimensions are implemented
3. Severity taxonomy is followed
4. Scan cadence supports on-change, daily, and weekly
5. Consumers can subscribe to the diagnostic stream
6. Diagnostic log is append-only with rotation
7. Every event includes a remediation_hint

## 9. Irreducible Context

- **Source paths:** `docs/corpus/ZK-072-journaling-protocol.md`, `docs/corpus/ZK-098-flight-recorder-mission-archive.md`, `docs/corpus/ZK-046-org-model-taste-over-headcount.md`, `docs/huan-standard/huan-spec-1.0.9.md`, `docs/huan-standard/huan-lifecycle-1.1.2.md`
- **Dependencies:** huan-spec v1.0.9 (card format, required fields as health check targets), huan-lifecycle v1.1.2 (status tiers, transition gates as diagnostic inputs)
- **Versions referenced:** ZK-072 (huan, 2026-05-06), ZK-098 (huan, 2026-05-08), ZK-046 (huan, 2026-04-05), huan-spec v1.0.9 (2026-05-15), huan-lifecycle v1.1.2 (2026-05-15)
- **Implementation:** Jepson Factory (reference runtime). NDJSON event emission, scan scheduling, consumer subscription.

---

*Lv25:10*
