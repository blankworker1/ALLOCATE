# M-NODE

Minimal demonstration experiment using core D-NODE hardware and dashboard.

Without the inclusion of industrial loads.

---

## M-Node Configuration

**Objective**

Create a Home Assistant live dashboard for a single node that shows energy allocation over 24 hours using real hardware. 

The system demonstrates 100% energy allocation efficiency, balancing PV generation, domestic load, battery charging/discharging, and flexible ASIC miners as surplus absorbers.

---

## 1. Allocatable Assets & Loads

Asset Type / Description / Control Type

PV Array, Single 2 kW trailer-mounted array, Cerbo GX

Battery Bank, 2–5 kWh battery,  BMS and level monitoring via Cerbo GX

Domestic Load, 6 x 10w smart light bulbs, ZigBee 

Flexible Load, 3 × NerdAxe Gamma ASIC miners, Braiins os dashboard app / API

---

## 2. Required Sensors

To fully monitor real hardware in Home Assistant:

Generation

sensor.pv_power – Instantaneous PV output (W)
sensor.pv_energy_today – Cumulative generation (Wh)

Storage
sensor.battery_voltage – V
sensor.battery_current – A
sensor.battery_soc – % state of charge
sensor.battery_power – W (charge/discharge)

Consumption

Domestic Load
sensor.domestic_power – Stepwise power (W)
sensor.domestic_energy – Cumulative energy (Wh)
Step schedule example:
Night baseline: 120 W
Daytime: 240 W
Evening peak: 300–360 W

Flexible Load (ASIC miners)
sensor.asic1_power, sensor.asic2_power, sensor.asic3_power – Individual (W)
sensor.asic_total_energy – Individual (Wh)

Step schedule: miners engage only if PV > Domestic + battery demand

Node Status / Connectivity
binary_sensor.node_connected – True if all hardware reporting
sensor.allocate_status – Dashboard state: Default, Green, Red

---

## 3. Allocation Logic

Priority Rules:

Serve domestic load at all times.

Charge battery until SOC target met.

Activate ASIC miners only if PV exceeds domestic load + battery charge. 

Step miners on/off according to available surplus.

Visualization:

24 hr graph of PV generation (bell curve), battery SOC (secondary axis), domestic load (step), and ASIC miners (step/variable).

Clock ring visualization (10-minute blocks) with day/night shading.

Allocation percentages for battery and miners.

Status boxes for ALLOCATE and CONNECTIVITY.

Efficiency:

Total PV is always allocated: domestic + battery + miners → demonstrates 100% allocation efficiency.

---

## 4. Hardware Integration

PV Inverter: Victron Multi Plus 3kw + Cerbo GX

Battery: Smart controller with SOC, voltage, and current reporting

Domestic Load: Smart light bulbs 

Flexible Load: NerdAxe ASIC miners with smart sockets

Home Assistant: Green + ZigBee mesh router

---

## 5. Dashboard Layout

Main Graph: PV generation (curve), battery SOC (secondary axis), domestic load (step), ASIC miners (step).

Clock Ring: 24 hr view with 10 min blocks, showing allocation in time.

Status Boxes:
ALLOCATE – Default (white), Green (working), Red (out-of-parameter)

CONNECTIVITY – Default (white), CONNECTED (green), DISCONNECTED (red)

---

## 6. Data Flow

Hardware to sensor to dashboard

PV → sensor → HA

Battery → BMS / BMS712 load monitor → HA

Domestic load → smart light bulbs → HA

ASIC miners → smart sockets → HA

All data represents real, physical energy flows, no simulation.

---

## 7. Optional Enhancements

Alerts

Historical data display (allocation efficiency over multiple days)

---

## M-Node Implementation Steps

Install Home Assistant Core on Green hardware device.

Connect PV Inverter & Battery via Cerbo GX device.

Connect ZigBee router for live readings from smart sockets and bulbs.

Connect domestic loads (light bulbs).

Connect Nerdaxe ASIC miners to smart sockets.

Copy YAML into configuration.yaml, restart HA.

Install ApexCharts Card (HACS) for time-series visualization.

Verify sensors are reporting real values: PV, battery SOC, domestic load.

Configure step schedule for domestic load in HA templates.

Test ASIC logic: miners should only turn on if PV exceeds domestic + battery demand.

Observe dashboard over 24 hr period. PV curve, battery SOC, domestic load steps, and ASIC load steps should match graph prompt.


---

## Home Assistant YAML

```

# ----------------------------
# 1. Sensors
# ----------------------------

# PV Array
sensor:
  - platform: template
    sensors:
      pv_power:
        friendly_name: "PV Power"
        unit_of_measurement: "W"
        value_template: "{{ states('sensor.inverter_power') | float }}"
      pv_energy_today:
        friendly_name: "PV Energy Today"
        unit_of_measurement: "Wh"
        value_template: "{{ states('sensor.inverter_energy') | float }}"

# Battery
  - platform: template
    sensors:
      battery_voltage:
        friendly_name: "Battery Voltage"
        unit_of_measurement: "V"
        value_template: "{{ states('sensor.battery_v') | float }}"
      battery_current:
        friendly_name: "Battery Current"
        unit_of_measurement: "A"
        value_template: "{{ states('sensor.battery_i') | float }}"
      battery_power:
        friendly_name: "Battery Power"
        unit_of_measurement: "W"
        value_template: "{{ (states('sensor.battery_v') | float) * (states('sensor.battery_i') | float) }}"
      battery_soc:
        friendly_name: "Battery SOC"
        unit_of_measurement: "%"
        value_template: "{{ states('sensor.battery_soc_raw') | float }}"

# Domestic Load
  - platform: template
    sensors:
      domestic_power:
        friendly_name: "Domestic Load Power"
        unit_of_measurement: "W"
        value_template: "{{ states('sensor.domestic_total') | float }}"
      domestic_energy:
        friendly_name: "Domestic Load Energy"
        unit_of_measurement: "Wh"
        value_template: "{{ states('sensor.domestic_total_energy') | float }}"

# Flexible ASIC Miners
  - platform: template
    sensors:
      asic1_power:
        friendly_name: "ASIC1 Power"
        unit_of_measurement: "W"
        value_template: "{{ states('switch.asic1') | float * 700 }}"  # assume 700W each
      asic2_power:
        friendly_name: "ASIC2 Power"
        unit_of_measurement: "W"
        value_template: "{{ states('switch.asic2') | float * 700 }}"
      asic3_power:
        friendly_name: "ASIC3 Power"
        unit_of_measurement: "W"
        value_template: "{{ states('switch.asic3') | float * 700 }}"
      asic_total_power:
        friendly_name: "Total ASIC Power"
        unit_of_measurement: "W"
        value_template: "{{ (states('sensor.asic1_power') | float) + (states('sensor.asic2_power') | float) + (states('sensor.asic3_power') | float) }}"

# Node Connectivity
binary_sensor:
  - platform: template
    sensors:
      node_connected:
        friendly_name: "Node Connected"
        value_template: >
          {{ states('sensor.pv_power')|float > 0
             and states('sensor.battery_soc')|float >= 0
             and states('sensor.domestic_power')|float > 0 }}

```

```

# ----------------------------
# 2. Switches for Flexible Load
# ----------------------------
switch:
  - platform: template
    switches:
      asic1:
        friendly_name: "ASIC Miner 1"
        value_template: "{{ is_state('switch.asic1', 'on') }}"
        turn_on:
          service: switch.turn_on
          target:
            entity_id: switch.relay_asic1
        turn_off:
          service: switch.turn_off
          target:
            entity_id: switch.relay_asic1
      asic2:
        friendly_name: "ASIC Miner 2"
        value_template: "{{ is_state('switch.asic2', 'on') }}"
        turn_on:
          service: switch.turn_on
          target:
            entity_id: switch.relay_asic2
        turn_off:
          service: switch.turn_off
          target:
            entity_id: switch.relay_asic2
      asic3:
        friendly_name: "ASIC Miner 3"
        value_template: "{{ is_state('switch.asic3', 'on') }}"
        turn_on:
          service: switch.turn_on
          target:
            entity_id: switch.relay_asic3
        turn_off:
          service: switch.turn_off
          target:
            entity_id: switch.relay_asic3

```

```
# ----------------------------
# 3. Dashboard / Lovelace
# ----------------------------
views:
  - title: "D-NODE Minimal"
    path: "dnode_minimal"
    badges:
      - entity: sensor.pv_power
      - entity: sensor.battery_soc
      - entity: binary_sensor.node_connected
    cards:
      - type: custom:apexcharts-card
        header:
          show: true
          title: "24h Energy Allocation"
        graph_span: 1d
        series:
          - entity: sensor.pv_power
            name: "PV Generation"
            type: line
            color: "#FFD700"
          - entity: sensor.domestic_power
            name: "Domestic Load"
            type: column
            color: "#4CAF50"
          - entity: sensor.asic_total_power
            name: "ASIC Load"
            type: column
            color: "#FF9800"
          - entity: sensor.battery_soc
            name: "Battery SOC"
            type: line
            yaxis_id: secondary
            color: "#2196F3"
      - type: entities
        title: "Flexible Load Control"
        entities:
          - switch.asic1
          - switch.asic2
          - switch.asic3
      - type: entities
        title: "Status Indicators"
        entities:
          - entity: binary_sensor.node_connected
          - entity: sensor.allocate_status

```

## Camera as a Sensor

Using a PTZ security camera integrated with Home Assistant allows the camera to trigger automations, detect tampering and environmental conditions and display camera live feed on the dashboard.



**Examples**

Use camera detect motion feature to send an alert via Home Assistant.

Use camera day/night status change for automatic scheduling of "dawn" trigger for domestic loads  (physics-based scheduling).

Upload screen images to dashboard so users can see miners running, battery indicators, PV panels, or smart sockets activity.


**Benefits**

Automatic scheduling: Node responds to real light levels rather than fixed hours.

Physically grounded: Ties allocation decisions directly to real-world energy input (sunlight).

Flexible & Scalable: Works for single-node demo or multiple nodes in different time zones/latitudes.

Low maintenance: No need to update clocks or daylight saving manually.

This makes the concept of energy allocation and hardware operation tangible.

The camera feed becomes part of the “living node” story.





