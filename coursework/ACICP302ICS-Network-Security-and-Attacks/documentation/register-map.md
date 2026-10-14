# ACICP302ICS — Verified Modbus Register Map

Course source commit:
2a66f9bcf253eb3fe31c68ad52794cd535421da8

| Register | Variable | Raw safe range | Engineering range | Initial |
|---|---|---|---|---|
| 0 | Electrolyzer temperature | 600-750 | 60.0-75.0 °C | 67.0 °C |
| 1 | Tank pressure | 300-400 | 30.0-40.0 bar | 34.0 bar |
| 2 | H2 flow rate | 500-1500 | 50.0-150.0 Nm3/h | 90.0 Nm3/h |
| 3 | Alarm | 0/1 | Boolean | 0 |

Registers 0-2 use a scale factor of 0.1.

Normal source-defined movement per one-second update:
- Temperature: approximately +/-0.2 °C
- Pressure: approximately +/-0.3 bar
- Flow: approximately +/-1.0 Nm3/h

Plant alarm is asserted when pressure reaches approximately 39.5 bar.

Normal baseline observation:
- Direct dashboard showed approximately 71.9 °C, 30.2 bar and 88.0 Nm3/h.
- Guarded dashboard showed approximately 72.6 °C, 30.1 bar and 89.6 Nm3/h.
- Both dashboards indicated normal/protected operation.
- Guard event view contained no attack events at baseline.

All documented services were bound to 127.0.0.1.
