# ACICP302ICS — Scenario 1 Analysis: Out-of-Range Pressure Hold

## Supplied Script

`attack_hold.py`

Authorized target:
`127.0.0.1` only

Direct path:
`127.0.0.1:5020`

Guarded path:
`127.0.0.1:5021`

## Direct-Path Observation

Primary direct execution:

- Writes sent: 75
- Peak pressure observed: 95.0 bar
- Source-defined safe pressure range: 30.0-40.0 bar
- Unsafe readings: 75/75 (100%)
- Script result: `UNSAFE VALUE REACHED THE PLANT`

An inadvertent duplicate direct-path execution also occurred:

- Writes sent: 76
- Peak pressure observed: 95.0 bar
- Unsafe readings: 74/76 (97%)

The first execution is used as the primary direct-path evidence.

## Guarded-Path Observation

- Writes sent: 76
- Peak pressure observed: 37.3 bar
- Unsafe readings: 0/76 (0%)
- Script result: `value never left safe range — attack fully contained`

## Guard Event Evidence

The guard logged repeated rejection reasons including:

- requested pressure 95.0 bar outside the 30.0-40.0 bar safe range;
- approximately 58 bar single-step change exceeding the 5.0 bar maximum;
- approximately 58 bar cumulative drift exceeding the 2.0 bar rolling-drift threshold.

## Interpretation

The direct plant path on port 5020 accepted the supplied out-of-range pressure request and therefore bypassed the validation control.

The same supplied request sent through the guarded path on port 5021 did not produce an unsafe observed pressure.

This validates the source-derived finding that the guard rejects writes that fail its range, step-size and rolling-drift checks.

It also validates the architectural risk that direct access to port 5020 bypasses guard enforcement.

## Recovery

After the direct scenario, all four documented services remained listening on their loopback addresses:

- 127.0.0.1:5020
- 127.0.0.1:5021
- 127.0.0.1:8080
- 127.0.0.1:8081

A normal process baseline must be confirmed before Scenario 2.
