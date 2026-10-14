# ACICP302ICS — Scenario 2 Execution Log

```text
ACICP302ICS — Scenario 2: slow_drift
====================================
Timestamp: 2026-10-14T18:20:46+01:00

Supplied script: slow_drift_attack.py
Direct target: 127.0.0.1:5020
Guarded target: 127.0.0.1:5021

New guard events since Scenario 2 baseline:
{"timestamp": "2026-10-14 18:18:12", "reason": "40.7 bar outside safe range 30.0-40.0 bar"}
{"timestamp": "2026-10-14 18:18:14", "reason": "41.7 bar outside safe range 30.0-40.0 bar"}
{"timestamp": "2026-10-14 18:18:16", "reason": "42.7 bar outside safe range 30.0-40.0 bar; cumulative drift of 3.0 bar over last 3 accepted writes exceeds 2.0 bar limit"}
{"timestamp": "2026-10-14 18:18:18", "reason": "43.7 bar outside safe range 30.0-40.0 bar; cumulative drift of 3.8 bar over last 3 accepted writes exceeds 2.0 bar limit"}
{"timestamp": "2026-10-14 18:18:20", "reason": "44.7 bar outside safe range 30.0-40.0 bar; cumulative drift of 4.7 bar over last 3 accepted writes exceeds 2.0 bar limit"}
{"timestamp": "2026-10-14 18:18:22", "reason": "45.7 bar outside safe range 30.0-40.0 bar; step of 5.8 bar exceeds max 5.0 bar; cumulative drift of 5.7 bar over last 3 accepted writes exceeds 2.0 bar limit"}
{"timestamp": "2026-10-14 18:18:24", "reason": "46.7 bar outside safe range 30.0-40.0 bar; step of 6.7 bar exceeds max 5.0 bar; cumulative drift of 6.8 bar over last 3 accepted writes exceeds 2.0 bar limit"}
{"timestamp": "2026-10-14 18:18:26", "reason": "47.7 bar outside safe range 30.0-40.0 bar; step of 8.0 bar exceeds max 5.0 bar; cumulative drift of 7.7 bar over last 3 accepted writes exceeds 2.0 bar limit"}
{"timestamp": "2026-10-14 18:18:28", "reason": "48.7 bar outside safe range 30.0-40.0 bar; step of 9.3 bar exceeds max 5.0 bar; cumulative drift of 9.0 bar over last 3 accepted writes exceeds 2.0 bar limit"}
```
