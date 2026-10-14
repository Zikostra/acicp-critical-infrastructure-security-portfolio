# ACICP302ICS — Supplied OT Guard Analysis

## Guard Role

The supplied `guard.py` acts as a rule-based Modbus/TCP validation proxy.

Plant:
127.0.0.1:5020

Guard:
127.0.0.1:5021

The guard is an educational control and is not a production process-safety system.

## Decision Table

| Check | Source-defined condition | Action on failure |
|---|---|---|
| Absolute range | Requested value outside allowed process range | Reject write and record event |
| Step-size | Requested change exceeds maximum permitted single step | Reject write and record event |
| Rolling drift | Requested value differs from oldest accepted value in 3-value history by more than drift threshold | Reject write and record event |
| Accepted write | All applicable checks pass | Forward to plant, update local mirror, append accepted history |
| Other register | Address is not temperature, pressure or flow | Pass through without the same process validation |

## Source-defined Thresholds

Temperature:
- Range: 60.0-75.0 °C
- Maximum step: 3.0 °C
- Drift threshold: 2.0 °C

Pressure:
- Range: 30.0-40.0 bar
- Maximum step: 5.0 bar
- Drift threshold: 2.0 bar

Flow:
- Range: 50.0-150.0 Nm3/h
- Maximum step: 10.0 Nm3/h
- Drift threshold: 4.0 Nm3/h

Rolling drift window:
3 accepted values

## Rejection Behaviour

When a protected write fails validation:
- the write is not forwarded to the plant;
- the guard mirror is not updated;
- the rejected value is not added to accepted-history state;
- an event is written to the local event log.

## Safe-State Synchronization

The guard periodically reads registers 0-3 from the real plant.

The mirror is updated only when temperature, pressure and flow are all within their absolute safe ranges.

Therefore the guarded dashboard can retain a last-known-safe state while the direct plant path is abnormal.

## Observed / Source-Derived Limitations

1. Direct access to port 5020 bypasses the guard.
2. No client authentication is implemented.
3. No client authorization policy is implemented.
4. No source/client identity policy is evident.
5. No replay/freshness mechanism is evident.
6. No demonstrated request-rate limiting is implemented.
7. Validation thresholds are process-specific.
8. Other registers are passed through without the same range/step/drift checks.
9. Guarded state can differ from actual direct-plant state during unsafe direct-path conditions.
10. The guard is not a process-safety system.

## Evidence

- `plant_sim/guard.py`
- `E03_Local_Service_Inventory.png`
- `risk-register.md`
- controlled validation evidence to follow
