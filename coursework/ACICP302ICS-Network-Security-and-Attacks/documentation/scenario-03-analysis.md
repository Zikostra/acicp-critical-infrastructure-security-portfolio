# ACICP302ICS — Scenario 3 Analysis: Replay / Freshness

## Supplied Script

`replay_attack.py`

Authorized target:
127.0.0.1 only

Direct path:
127.0.0.1:5020

Guarded path:
127.0.0.1:5021

## Direct-Path Observation

The direct-path execution replayed the same valid pressure write three times:

32.3 bar

No service failure occurred after the execution.

## Guarded-Path Observation

The guarded-path execution replayed the same valid pressure write three times:

33.2 bar

No new guard event was generated during the replay scenario.

## Interpretation

The guarded replay was not rejected.

This is consistent with the supplied guard design.

The guard validates:
- absolute process range;
- maximum single-step change;
- rolling-baseline drift.

The reviewed source does not implement an explicit:
- freshness check;
- sequence-number policy;
- duplicate-command check;
- anti-replay mechanism.

Because the repeated pressure value remained within the applicable process limits, the same valid value could be accepted repeatedly.

This does not mean the guard failed its implemented controls. Instead, the scenario demonstrates a limitation in the scope of those controls.

A stronger production design could supplement process-value validation with command freshness, authenticated client identity, sequence/session context, or replay-detection logic.

## Evidence

- E08A_Replay_Direct.png
- E08B_Replay_Guarded.png
- plant_sim/events.jsonl
