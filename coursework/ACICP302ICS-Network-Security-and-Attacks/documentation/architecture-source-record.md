# ACICP302ICS — Architecture and Source Record

```text
ACICP302ICS — Activity 01 Source Architecture
==============================================

Course commit: 2a66f9bcf253eb3fe31c68ad52794cd535421da8

=== PLANT ===
16:REG_TEMP = 0
17:REG_PRESSURE = 1
18:REG_FLOW = 2
19:REG_ALARM = 3
21:TEMP_RANGE = (600, 750)
22:PRESSURE_RANGE = (300, 400)
23:FLOW_RANGE = (500, 1500)
25:UPDATE_INTERVAL_SEC = 1.0
26:HOST = "127.0.0.1"
27:PORT = 5020
42:            REG_TEMP: 670,
43:            REG_PRESSURE: 340,
44:            REG_FLOW: 900,
67:        temp = clamp(block.get_internal(REG_TEMP) + random.randint(-2, 2), *TEMP_RANGE)
68:        pressure = clamp(block.get_internal(REG_PRESSURE) + random.randint(-3, 3), *PRESSURE_RANGE)
69:        flow = clamp(block.get_internal(REG_FLOW) + random.randint(-10, 10), *FLOW_RANGE)
71:        block.set_internal(REG_TEMP, temp)
72:        block.set_internal(REG_PRESSURE, pressure)
73:        block.set_internal(REG_FLOW, flow)
75:        store.setValues(3, REG_TEMP, [temp])
76:        store.setValues(3, REG_PRESSURE, [pressure])
77:        store.setValues(3, REG_FLOW, [flow])
79:        alarm = 1 if pressure >= PRESSURE_RANGE[1] - 5 else 0
80:        store.setValues(3, REG_ALARM, [alarm])
86:        time.sleep(UPDATE_INTERVAL_SEC)

=== GUARD ===
19:PLANT_HOST = "127.0.0.1"
20:PLANT_PORT = 5020
22:GUARD_PORT = 5021
24:REG_TEMP = 0
25:REG_PRESSURE = 1
26:REG_FLOW = 2
27:REG_ALARM = 3
29:TEMP_RANGE     = (600, 750)   # tenths of a degree C
30:PRESSURE_RANGE = (300, 400)   # tenths of a bar
31:FLOW_RANGE     = (500, 1500)  # tenths of Nm3/h
33:MAX_TEMP_STEP      = 30
34:MAX_PRESSURE_STEP  = 50
35:MAX_FLOW_STEP       = 100
40:# value from DRIFT_WINDOW writes ago. This catches cumulative creep even
42:DRIFT_WINDOW              = 3   # was 6 — shrinking cuts the attacker's runway in half
43:DRIFT_THRESHOLD_TEMP      = 20  # 2.0C cumulative over the window
44:DRIFT_THRESHOLD_PRESSURE  = 20  # 2.0 bar cumulative over the window
45:DRIFT_THRESHOLD_FLOW      = 40  # 4.0 Nm3/h cumulative over the window
84:        self.temp_accepted_history     = deque(maxlen=DRIFT_WINDOW)
85:        self.pressure_accepted_history = deque(maxlen=DRIFT_WINDOW)
86:        self.flow_accepted_history     = deque(maxlen=DRIFT_WINDOW)
105:        if len(drift_history) == DRIFT_WINDOW:
110:                    f"over last {DRIFT_WINDOW} accepted writes exceeds "
120:        if address == REG_TEMP:
121:            current = self.getValues(3, REG_TEMP, count=1)[0]
122:            reasons = self._check(address, requested, current, TEMP_RANGE,
123:                                   MAX_TEMP_STEP, self.temp_accepted_history,
124:                                   DRIFT_THRESHOLD_TEMP, "C", 10)
125:        elif address == REG_PRESSURE:
126:            current = self.getValues(3, REG_PRESSURE, count=1)[0]
127:            reasons = self._check(address, requested, current, PRESSURE_RANGE,
128:                                   MAX_PRESSURE_STEP, self.pressure_accepted_history,
129:                                   DRIFT_THRESHOLD_PRESSURE, " bar", 10)
130:        elif address == REG_FLOW:
131:            current = self.getValues(3, REG_FLOW, count=1)[0]
132:            reasons = self._check(address, requested, current, FLOW_RANGE,
133:                                   MAX_FLOW_STEP, self.flow_accepted_history,
134:                                   DRIFT_THRESHOLD_FLOW, " Nm3/h", 10)
163:        if address == REG_TEMP:
165:        elif address == REG_PRESSURE:
167:        elif address == REG_FLOW:
187:                    t, p, f = regs[REG_TEMP], regs[REG_PRESSURE], regs[REG_FLOW]
188:                    if (TEMP_RANGE[0]     <= t <= TEMP_RANGE[1] and
189:                        PRESSURE_RANGE[0] <= p <= PRESSURE_RANGE[1] and
190:                        FLOW_RANGE[0]     <= f <= FLOW_RANGE[1]):
201:    plant_client = ModbusTcpClient(PLANT_HOST, port=PLANT_PORT)
217:             HOST, GUARD_PORT, PLANT_HOST, PLANT_PORT)
219:        StartTcpServer(context=context, address=(HOST, GUARD_PORT))

=== DASHBOARDS ===
plant_sim/dashboard.py:6:TARGET_HOST = "127.0.0.1"
plant_sim/dashboard.py:7:TARGET_PORT = 5020
plant_sim/dashboard.py:201:    client = ModbusTcpClient(TARGET_HOST, port=TARGET_PORT)
plant_sim/dashboard.py:224:    app.run(host="127.0.0.1",port=8080)
plant_sim/dashboard_guarded.py:8:TARGET_HOST = "127.0.0.1"
plant_sim/dashboard_guarded.py:9:TARGET_PORT = 5021
plant_sim/dashboard_guarded.py:228:    client = ModbusTcpClient(TARGET_HOST, port=TARGET_PORT)
plant_sim/dashboard_guarded.py:265:    app.run(host="127.0.0.1",port=8081)
```
