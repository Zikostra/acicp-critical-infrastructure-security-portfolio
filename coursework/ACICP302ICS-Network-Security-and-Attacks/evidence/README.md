# ACICP302ICS — Evidence Gallery

All visual evidence below was collected from the authorized instructor-supplied local OT simulation.

**Authorized network scope:** `127.0.0.1`

---

## E01 — Preflight and Source Safety

![E01 — Preflight and Source Safety](screenshots/E01_Preflight_Source_Safety.png)

Canonical source, source commit and loopback-only safety verification.

---

## E02 — Normal Operating Baseline

![E02 — Normal Operating Baseline](screenshots/E02_Normal_Baseline.png)

Direct and guarded dashboards during normal process operation.

---

## E03 — Local Service Inventory

![E03 — Local Service Inventory](screenshots/E03_Local_Service_Inventory.png)

Authorized services listening on 127.0.0.1 only.

---

## E04 — Modbus/TCP Request and Response

![E04 — Modbus/TCP Request and Response](screenshots/E04_Modbus_Request_Response.png)

Selected Function Code 03 request/response used for packet analysis.

---

## E05 — Guard Rule Analysis

![E05 — Guard Rule Analysis](screenshots/E05_Guard_Rule_Analysis.png)

Source-defined absolute-range, maximum-step and rolling-drift controls.

---

## E06A — Attack Hold — Direct Path

![E06A — Attack Hold — Direct Path](screenshots/E06A_AttackHold_Direct.png)

Direct path reaching the supplied 95.0 bar value.

---

## E06B — Attack Hold — Guarded Path

![E06B — Attack Hold — Guarded Path](screenshots/E06B_AttackHold_Guarded.png)

Guarded path containment and detection evidence.

---

## E07A — Slow Drift — Direct Path

![E07A — Slow Drift — Direct Path](screenshots/E07A_SlowDrift_Direct.png)

Direct-path slow-pressure-drift observation.

---

## E07B — Slow Drift — Guarded Path

![E07B — Slow Drift — Guarded Path](screenshots/E07B_SlowDrift_Guarded.png)

Guard rejection events during the slow-drift scenario.

---

## E08A — Replay — Direct Path

![E08A — Replay — Direct Path](screenshots/E08A_Replay_Direct.png)

Repeated otherwise-valid direct write.

---

## E08B — Replay — Guarded Path

![E08B — Replay — Guarded Path](screenshots/E08B_Replay_Guarded.png)

Repeated otherwise-valid guarded write with no new guard event.

---

## E09 — Final Recovery Verification

![E09 — Final Recovery Verification](screenshots/E09_Final_Recovery.png)

Confirmation that the four laboratory ports were closed and supplied processes stopped.

---

## Additional Evidence

- [Normal Modbus/TCP packet capture](packets/normal_modbus.pcapng)
- [Final guard event log](logs/events-final.jsonl)
- [Normal service inventory](logs/normal-service-inventory.md)
- [Scenario 1 execution log](logs/scenario-01-attack-hold.md)
- [Scenario 2 execution log](logs/scenario-02-slow-drift.md)
- [Scenario 3 execution log](logs/scenario-03-replay.md)
