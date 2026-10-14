# ACICP302ICS — Local Exposure Record

## Authorized Scope

Observation target: local ACICP302 simulation only

Authorized address:
127.0.0.1

Observation method:
- supplied source-code inspection
- local listener inspection with `ss`
- no general network discovery
- no external network scanning

## Documented Services

| Component | Address | Port | Purpose |
|---|---|---:|---|
| Simulated plant | 127.0.0.1 | 5020 | Direct Modbus/TCP plant path |
| Validation guard | 127.0.0.1 | 5021 | Rule-based guarded Modbus/TCP path |
| Direct dashboard | 127.0.0.1 | 8080 | Direct process visualization |
| Guarded dashboard | 127.0.0.1 | 8081 | Guarded process visualization and event display |

## Observed State

All four services were observed listening only on 127.0.0.1.

No documented ACICP302 service was observed listening on:
- 0.0.0.0
- a LAN address
- an external interface

Evidence:
- E03_Local_Service_Inventory.png
- evidence/logs/normal-service-inventory.md

## Exposure Interpretation

Current loopback-only binding substantially limits exposure from external hosts.

However, source review shows that port 5020 provides a direct path to the simulated plant and does not pass through the validation guard on port 5021.

The dashboards do not implement authentication in the supplied simulation. Their current loopback-only binding reduces exposure, but broader binding would materially increase risk.

This is a source-code-guided educational simulation and is not a production OT security architecture.
