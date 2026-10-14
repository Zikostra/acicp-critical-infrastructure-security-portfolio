# ACICP302ICS — Controlled Security Validation Test Plan

Course commit:
2a66f9bcf253eb3fe31c68ad52794cd535421da8

Canonical source:
labs/ot-security/student-lab-source

Authorized scope:
127.0.0.1 only

## Safety Conditions

- Use only supplied scripts.
- Do not modify script parameters.
- Do not change addresses or ports.
- Run one scenario at a time.
- Establish normal baseline before each scenario.
- Compare direct path 5020 with guarded path 5021.
- Record actual output rather than attempting to force an expected result.
- No DoS demonstration will be performed without explicit instructor approval.

## Scenario 1 — Out-of-range pressure hold

Script:
attack_hold.py

Direct:
python3 attack_hold.py 5020

Guarded:
python3 attack_hold.py 5021

Expected direct-path behaviour:
The supplied out-of-range pressure request may reach the simulated plant.

Expected guarded behaviour:
The guard should reject the request due to absolute-range and/or step-size validation and create event evidence.

Evidence:
- script output
- direct dashboard
- guarded dashboard
- events.jsonl

Recovery:
Wait for normal plant simulation to return to a safe baseline and verify both views before proceeding.

## Scenario 2 — Slow pressure drift

Script:
slow_drift_attack.py

Direct:
python3 slow_drift_attack.py 5020

Guarded:
python3 slow_drift_attack.py 5021

Expected direct-path behaviour:
Incremental supplied pressure writes may influence the direct plant.

Expected guarded behaviour:
Individual writes may initially satisfy step-size rules, but rolling-baseline drift validation is expected to become relevant.

Actual result may vary because normal plant movement occurs concurrently.

Evidence:
- script output
- dashboards
- events.jsonl

Recovery:
Verify normal baseline before proceeding.

## Scenario 3 — Repeated valid pressure write

Script:
replay_attack.py

Direct:
python3 replay_attack.py 5020

Guarded:
python3 replay_attack.py 5021

Expected direct-path behaviour:
The supplied repeated pressure value may be accepted.

Expected guarded behaviour:
If the repeated value remains within range, step and drift thresholds, the guard may accept it because no explicit freshness or anti-replay mechanism is evident.

This scenario is intended to demonstrate a control limitation, not necessarily a guard rejection.

Evidence:
- script output
- dashboards
- events.jsonl

Recovery:
Verify normal baseline after completion.

## Stop Conditions

Stop immediately if:
- any script targets an address other than 127.0.0.1;
- an unexpected service or network destination appears;
- the supplied script differs materially from the reviewed canonical source;
- lab services become unstable outside the expected bounded scenario.

## Instructor Approval

Status:
Not independently evidenced in this record.

The learner must follow the instructor's approval requirements before executing controlled demonstrations.
