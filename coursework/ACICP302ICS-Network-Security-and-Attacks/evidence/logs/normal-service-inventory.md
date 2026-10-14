# ACICP302ICS — Normal Service Inventory

```text
ACICP302ICS — Normal Service Inventory
======================================
Timestamp: 2026-10-14T17:12:14+01:00

LISTEN 0      128        127.0.0.1:8080      0.0.0.0:*    users:(("python3",pid=6200,fd=4))
LISTEN 0      128        127.0.0.1:8081      0.0.0.0:*    users:(("python3",pid=6505,fd=3))
LISTEN 0      100        127.0.0.1:5020      0.0.0.0:*    users:(("python3",pid=5589,fd=6))
LISTEN 0      100        127.0.0.1:5021      0.0.0.0:*    users:(("python3",pid=5903,fd=7))

Conclusion:
All documented ACICP302 services are bound to Linux loopback 127.0.0.1.
No documented service is listening on 0.0.0.0 or a non-loopback host address.
```
