# M-NODE

Minimal demonstration experiment using core D-NODE hardware and dashboard. Without the inclusion of industrial loads.


## M-Node Configuration

**Objective**

Create a Home Assistant live dashboard for a single node that shows energy allocation over 24 hours using real hardware. 

The system demonstrates 100% energy allocation efficiency, balancing PV generation, domestic load, battery charging/discharging, and flexible ASIC miners as surplus absorbers.

---

## 1. Allocatable Assets & Loads

Asset Type / Description / Control Type
PV Array, Single 2 kW trailer-mounted array, Cerbo GX
Battery Bank, 2–5 kWh battery,  BMS and level monitoring via Cerbo GX Sensor
Domestic Load 6 x 10w smart light bulbs, ZigBee 
Flexible Load, 3 × NerdAxe Gamma ASIC miners, Braiins os dashboard app / API

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







