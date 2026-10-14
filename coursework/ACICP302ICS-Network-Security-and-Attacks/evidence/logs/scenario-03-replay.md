# ACICP302ICS — Scenario 3 Execution Log

```text
ACICP302ICS — Scenario 3: Replay / Freshness
============================================

Supplied script:
replay_attack.py

Direct target:
127.0.0.1:5020

Observed direct result:
Replayed write 32.3 bar three times.

Guarded target:
127.0.0.1:5021

Observed guarded result:
Replayed write 33.2 bar three times.

New guard events during guarded replay:
None observed.

Conclusion:
The supplied guard did not distinguish the repeated otherwise-valid write as a replay.
```
