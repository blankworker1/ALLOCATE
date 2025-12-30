# D-NODE Hardware

Minimum Hardware Requirements based on:

- 1:10 scaling of average domestic consumption in Italy

- off-grid installation using Victron equipment

- monitoring, control and display via Home Assistant

### 1. PV Generation

PV panels

6 × ~400–450 W panels (48 V nominal)

Mounted outdoors, individual strings


PV protection & isolation

6 × DC PV isolators / breakers

≥ 150 V DC rated

≥ 15–20 A

Manual operation (you already selected these)



Charge control

1 × MPPT charge controller

Victron SmartSolar MPPT

Input voltage compatible with panel Voc

Output: 48 V battery system


Optional (for teaching clarity): 1 MPPT per 2–3 panels, but not required



---

### 2. Energy storage

Battery

48 V battery bank

LiFePO₄ preferred (safety + cycle life)

Capacity: 5–10 kWh

Enough to carry night + morning loads



Integrated or external BMS


Battery protection

Main DC battery breaker

≥ 125 A DC rated


DC busbars

Positive & negative


Class-T or MEGA fuse (optional but recommended)



---

## 3. Inverter / system backbone

Inverter–charger

Victron MultiPlus-II or Quattro

48 V system

3–5 kVA is sufficient for demo


Handles:

AC generation

Load supply

Battery charging/discharging



AC distribution

AC breaker panel

Separate breakers for:

Domestic loads

Industrial loads

ASIC load



RCD / RCBO for safety



---

### 4. Control & monitoring

Energy monitoring

Victron Cerbo GX

Central system monitor

Links MPPT, inverter, battery



Communications

VE.Direct / VE.Bus cables

Ethernet or Wi-Fi uplink



---

### 5. Load control

Home automation

Home Assistant Green

Zigbee coordinator (ZBT-2)

Sensors


**Domestic loads**

Lighting cluster to represent each home

36 × 10 W ZigBee bulbs

6 homes × 6 bulbs

ZigBee groups per household

No additional relays required



**Industrial loads**

For pasta making + restaurant

Minimum controllable load blocks:

Function	Hardware

Milling	1 resistive load + SSR
Mixing	1 resistive load + SSR
Extrusion	1 resistive load + SSR
Dehydration	1–2 resistive loads + SSRs
Packaging	1 resistive load + SSR
Plate washing	1 resistive load + SSR


Resistive load elements (heaters / dummy loads)

DC-controlled SSRs or contactors

AC side switching only

Controlled via ZigBee relay or GPIO




**ASIC flexible surplus loads**

Minimum viable setup:

1–2 ASIC miners

Combined draw: ~2–2.5 kW


OR resistive load bank if you want silence


Control:

AC contactor or SSR

Controlled via ZigBee relay

Enabled only when PV surplus exists



---

### 6. Safety & enclosure

Enclosures

Outdoor-rated PV combiner / isolator boxes

Indoor IP-rated cabinet for:

MPPT

Inverter

Battery

DC bus



Grounding

Earth rod

Bond:

PV frames

Inverter

Enclosures



Cabling

PV DC cable (UV rated)

Battery cables (appropriately sized)

AC cabling with ferrules and glands



---

### 7. Minimum equipment summary

At absolute minimum you need:

6 PV panels

6 DC PV isolators

1 MPPT

1 48 V battery

1 Victron inverter

1 Cerbo GX

1 Home Assistant Green + ZigBee

ZigBee bulbs for domestic load

SSR-controlled resistive loads for industrial processes

One flexible high-power load (ASIC or dummy load)



---

### 8. Why this is the minimum and not overbuilt

No grid connection required

No PV switching under load (manual isolation only)

No unnecessary smart relays on DC side

Clear functional separation:

Generation

Storage

Mandatory load

Productive load

Flexible load




---


**TO DO**

1. Produce a single-line electrical diagram


2. Size breakers, fuses, and cables precisely


3. Design Home Assistant automations (PV-aware load scheduling)


