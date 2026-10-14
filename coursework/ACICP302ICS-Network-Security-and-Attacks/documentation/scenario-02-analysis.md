# ACICP302ICS — Scenario 2 Analysis: Slow Pressure Drift

## Supplied Script

`slow_drift_attack.py`

Direct path:
`127.0.0.1:5020`

Guarded path:
`127.0.0.1:5021`

## Direct-Path Observation

The direct run began at approximately 37.8 bar.

The supplied script incrementally requested higher pressure values, including:

- 38.8 bar -> observed approximately 39.0 bar
- 39.8 bar -> observed approximately 40.0 bar
- 40.8 bar -> observed approximately 40.0 bar
- 41.8 bar -> observed approximately 39.7 bar
- 42.8 bar -> observed approximately 39.7 bar
- later requests continued upward toward approximately 48.8 bar while observed readings remained near the upper safe boundary.

The direct-path result differs from Scenario 1 because the slow-drift script waits between writes. During those intervals, the plant simulation's periodic process-update logic continues running and clamps pressure into its source-defined 30.0-40.0 bar range.

Therefore, the observed safe readback on the direct path does not demonstrate guard protection. It reflects interaction between the supplied write timing and the plant's own simulation/update behaviour.

## Guarded-Path Observation

The guarded run began at approximately 36.7 bar.

Early requests inside the safe range were reflected in process readings.

Examples:

- requested 37.7 bar -> observed approximately 37.8 bar
- requested 38.7 bar -> observed approximately 38.4 bar
- requested 39.7 bar -> observed approximately 39.9 bar

Once requests exceeded the source-defined 40.0 bar pressure limit, observed guarded pressure remained approximately 39-40 bar.

## Guard Event Evidence

The guard recorded:

- 40.7 bar: outside safe range
- 41.7 bar: outside safe range
- 42.7 bar: outside safe range and 3.0 bar cumulative drift
- later requests: increasing cumulative-drift violations
- from 45.7 bar onward: step-size violations also became applicable

The source-defined pressure controls are:

- absolute range: 30.0-40.0 bar
- maximum single step: 5.0 bar
- rolling drift threshold: 2.0 bar
- rolling window: 3 accepted values

## Interpretation

The scenario demonstrates layered guard behaviour.

Absolute-range validation became the first explicit rejection condition once the requested pressure exceeded 40.0 bar.

As rejected writes accumulated while the accepted baseline remained safe, the rolling-baseline drift difference increased and subsequently triggered the drift rule.

At larger requested differences, the single-step rule also became applicable.

The scenario also demonstrates why direct-path readback must be interpreted alongside plant timing. The direct plant's periodic simulation update can normalize pressure before the script reads the value back.

## Evidence

- E07A_SlowDrift_Direct.png
- E07B_SlowDrift_Guarded.png
- evidence/logs/scenario-02-slow-drift.md
- plant_sim/events.jsonl
