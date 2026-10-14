# ACICP302ICS — Evidence Index

Course source commit:
`2a66f9bcf253eb3fe31c68ad52794cd535421da8`

Authorized simulation scope:
`127.0.0.1`

## Preflight and Baseline

| Evidence ID | File | Purpose |
|---|---|---|
| E01 | E01_Preflight_Source_Safety.png | Shows canonical source, exact commit, prohibited-address check and loopback configuration |
| E02 | E02_Normal_Baseline.png | Shows direct and guarded dashboards operating normally before controlled validation |
| E03 | E03_Local_Service_Inventory.png | Shows services bound to 127.0.0.1 on ports 5020, 5021, 8080 and 8081 |
| E04 | E04_Modbus_Request_Response.png | Shows selected normal Modbus/TCP FC03 request/response transaction |
| E05 | E05_Guard_Rule_Analysis.png | Shows source-defined absolute-range, step-size and rolling-drift rules |

## Controlled Validation

| Evidence ID | File | Purpose |
|---|---|---|
| E06A | E06A_AttackHold_Direct.png | Direct-path out-of-range pressure demonstration |
| E06B | E06B_AttackHold_Guarded.png | Guarded-path containment and detection evidence |
| E07A | E07A_SlowDrift_Direct.png | Direct-path slow-drift observation |
| E07B | E07B_SlowDrift_Guarded.png | Guarded slow-drift behaviour and event evidence |
| E08A | E08A_Replay_Direct.png | Direct repeated-write demonstration |
| E08B | E08B_Replay_Guarded.png | Guarded repeated-write demonstration showing replay/freshness limitation |

## Recovery

| Evidence ID | File | Purpose |
|---|---|---|
| E09 | E09_Final_Recovery.png | Confirms all ACICP302 ports closed and supplied lab processes stopped |

## Packet and Log Evidence

- `evidence/packets/normal_modbus.pcapng`
- `evidence/logs/normal-service-inventory.md`
- `evidence/logs/scenario-01-attack-hold.md`
- `evidence/logs/scenario-02-slow-drift.md`
- `evidence/logs/scenario-03-replay.md`
- `evidence/logs/events-final.jsonl`

## Supporting Documentation

- `preflight-record.md`
- `register-map.md`
- `modbus-packet-analysis.md`
- `local-exposure-record.md`
- `risk-register.md`
- `guard-analysis.md`
- `validation-test-plan.md`
- `scenario-01-analysis.md`
- `scenario-02-analysis.md`
- `scenario-03-analysis.md`
- `recovery/recovery-verification.md`

## Environment Deviation

The practical work was performed using a dedicated non-sudo Ubuntu user account on the learner's Ubuntu host rather than the fresh guest VM described in the course guide.

All supplied simulation services and controlled demonstrations remained bound to `127.0.0.1`.
