
# D-NODE Process Overview

This section details the energy-intensive, schedulable components of the D-NODE microgrid demo. Together, the industrial and flexible loads demonstrate how a microgrid can prioritize essential production while efficiently absorbing excess generation, minimizing energy curtailment, and integrating real-world farm operations with renewable energy.



**1. Industrial Loads (Real-World Testing)**

Purpose: On-farm pasta production and restaurant service.

Equipment: Milling, dough mixing, pasta extrusion, dehydration, packaging, restaurant cooking.

Measurement: Real kW draw monitored and recorded during operations.

Scheduling: Midday, aligned with PV peak for maximum solar utilization (priority 2).

Function in system: Demonstrates productive use of PV energy and the concept of scheduling and allocation of loads to match renewable generation.

**2.Flexible Loads (Load Balancing)**

Purpose: Consume any PV surplus not used by domestic or industrial loads.

Equipment: ASIC miners.

Control: Enabled only when PV generation exceeds other load requirements (priority 3).

Function in system: Prevents curtailment, demonstrates demand-side flexibility, and balances the system.

## System Design Highlights

Generation: 6 × 400–450 W PV panels feeding a Victron MPPT → 48 V LiFePO₄ battery → inverter → AC loads.

Control & Monitoring: Home Assistant Green + Zigbee coordinator, Victron Cerbo GX for energy monitoring.

Load Prioritization: Domestic (always on, educational), Industrial (PV-aligned, real energy), Flexible / ASIC (PV surplus only)

Battery Role: Buffers night and morning loads, enables smooth load supply.

## Educational + Operational Integration

Visitors can see 

- how energy flows from PV to different loads.

- How industrial processes respond to solar availability, and how flexible loads can absorb surplus energy.

The setup simultaneously demonstrates microgrid concepts and operates a real on-farm pasta production workshop and restaurant, with measurable energy consumption and production efficiency.




