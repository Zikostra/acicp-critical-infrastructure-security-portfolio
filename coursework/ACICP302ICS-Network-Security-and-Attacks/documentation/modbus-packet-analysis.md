# ACICP302ICS — Normal Modbus/TCP Packet Analysis

## Capture

Interface: Linux loopback (`lo`)
Capture filter: `tcp port 5020`
Evidence file: `evidence/packets/normal_modbus.pcapng`
Packets captured: 66
Packets dropped: 0

Only the documented local Modbus plant service on 127.0.0.1:5020 was captured.

## Selected Request / Response

Request frame: 1
Response frame: 2
Transaction Identifier: 669
Unit Identifier: 1
Function Code: 03 — Read Holding Registers

Client:
127.0.0.1:45670

Plant server:
127.0.0.1:5020

Observed request payload:

029d00000006010300000004

Decoded request:
- Transaction ID: 669
- Protocol ID: 0
- Unit ID: 1
- Function Code: 03
- Starting holding register: 0
- Quantity: 4 registers

Observed response payload:

029d0000000b01030802cc015c043b0000

Decoded response:
- Transaction ID: 669
- Function Code: 03
- Byte count: 8
- Register 0: 0x02cc = 716 = 71.6 °C
- Register 1: 0x015c = 348 = 34.8 bar
- Register 2: 0x043b = 1083 = 108.3 Nm3/h
- Register 3: 0x0000 = 0 = alarm off

Observed request-to-response interval was approximately 0.582 ms.

## Interpretation

The captured traffic confirms that the normal dashboard/client reads four consecutive
holding registers beginning at address 0.

The returned values correspond directly to the source-defined process data model:
temperature, pressure, hydrogen flow and alarm status.

Registers 0 through 2 use a scale factor of 0.1. The observed values were within the
source-defined normal ranges and the alarm register was clear.

The request and response remained entirely on 127.0.0.1, consistent with the
authorized loopback-only lab scope.
