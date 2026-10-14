# ACICP302ICS — Network Security & Attacks

## OT / ICS Network Security Practical Assessment

This directory contains the learner-produced documentation, evidence, packet capture, controlled validation records, recovery verification, and final assessment report for the ACICP302ICS practical assessment.

## Submission Navigation

- **[Final Assessment Report](FINAL_ASSESSMENT_REPORT.md)**
- **[Evidence Gallery](evidence/README.md)**
- **[Documentation Index](documentation/README.md)**
- **[Risk Register](documentation/risk-register.md)**
- **[Final Recovery Verification](recovery/recovery-verification.md)**

## Instructor Source

Instructor repository: `icdfa/ACICP302ICS-Network-Security-and-Attacks`

Canonical runnable source: `labs/ot-security/student-lab-source/`

Source commit: `2a66f9bcf253eb3fe31c68ad52794cd535421da8`

The instructor-provided laboratory source code is not reproduced in this portfolio.

## Authorized Scope

All simulation and validation activity remained restricted to `127.0.0.1`.

| Component | Endpoint | Purpose |
|---|---|---|
| Simulated plant | `127.0.0.1:5020` | Direct Modbus/TCP plant interface |
| Validation guard | `127.0.0.1:5021` | Process-aware validation proxy |
| Direct dashboard | `127.0.0.1:8080` | Direct plant monitoring |
| Guarded dashboard | `127.0.0.1:8081` | Guarded monitoring and event visibility |

No external system was targeted.

## Assessment Activities

- Preflight and source-safety verification
- OT architecture and data-flow analysis
- Modbus/TCP register mapping
- Normal-operation baseline capture
- Modbus/TCP packet capture and analysis
- Local service exposure assessment
- ICS risk-register development
- Validation-guard analysis
- Controlled direct-versus-guarded testing
- Recovery and cleanup verification

## Controlled Validation Scenarios

### Scenario 1 — Out-of-Range Pressure Hold

The direct path reached `95.0 bar` against a defined safe range of `30.0–40.0 bar`. The first direct run produced `75/75` unsafe readings.

The guarded path produced `0/76` unsafe readings, with a peak observed pressure of approximately `37.3 bar`. Guard events recorded range, step-size, and rolling-drift violations.

### Scenario 2 — Slow Pressure Drift

The guarded path accepted initial in-range requests and rejected later requests that exceeded configured process limits. Logged events demonstrated absolute-range, rolling-drift, and step-size controls.

### Scenario 3 — Replay / Freshness

The direct path replayed `32.3 bar` three times. The guarded path replayed `33.2 bar` three times and generated no new guard event.

This demonstrates that the supplied guard does not implement explicit freshness or anti-replay validation.

## Principal Findings

1. Direct access to port `5020` bypasses guard enforcement.
2. The supplied Modbus interface does not implement client authentication or authorization.
3. Writable process registers can influence simulated process state.
4. The guard blocks writes that violate configured process rules.
5. Rejected writes are recorded in the guard event log.
6. The guarded mirror may retain last-known-safe values while plant state differs.
7. Explicit replay/freshness protection is not implemented.
8. Non-protected registers do not receive equivalent process validation.

## Evidence

See [`documentation/evidence-index.md`](documentation/evidence-index.md).

Evidence includes screenshots E01–E09, Modbus/TCP PCAP data, scenario logs, guard events, risk analysis, validation analysis, and recovery verification.

## Environment Methodology Note

The course guide recommended a fresh isolated Ubuntu VM. This practical instead used a dedicated non-sudo Ubuntu account on the learner Ubuntu host.

This provided account-level separation but is not equivalent to VM isolation because the kernel and loopback networking remained host-shared.

All laboratory services remained bound to `127.0.0.1`.

## Recovery

At completion, ports `5020`, `5021`, `8080`, and `8081` were closed and no supplied ACICP302 lab processes remained running.

See [`recovery/recovery-verification.md`](recovery/recovery-verification.md).

## Safety and Ethics

All activity was conducted solely against the instructor-supplied local simulation.

The supplied denial-of-service scenario was not executed.

No external ICS, SCADA, OT, public, or third-party system was targeted.
