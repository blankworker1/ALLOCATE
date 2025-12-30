
# D-NODE

## Physical Allocation Node Demonstration 

The D-NODE is a small, real-world energy system designed to make allocation visible, measurable, and unavoidable.

It is not a simulation. It is a working solar-powered microgrid that receives energy, stores some of it, consumes some of it, and transforms any remaining surplus.

Every watt that enters the system must be allocated in time. Nothing is assumed. Nothing is hidden. 

The purpose of the node is to demonstrate, in physical hardware, the core idea of Allocation Economics: economic outcomes are the result of allocation decisions made under real constraints.

The node models a rural microgrid using three prioritized load classes: 

- **Domestic** (reliability-critical) Domestic loads represent non-negotiable human needs that must always be served.

- **Industrial** (productive and schedulable) Industrial loads represent useful work that can be scheduled to align with energy availability.

- **Load Balancing** a fully flexible surplus sink that represents optional transformation. A place for energy that would otherwise be curtailed or wasted, without creating stress elsewhere in the system. 

These loads are intentionally different in character.

Together, these layers show how variable solar generation can be balanced through design rather than overbuilding storage or curtailing production.

The D-NODE does not attempt to optimize for profit, efficiency, or ideological goals. 

Its purpose is clarity. By exposing energy flows, time dependence, and priority decisions in a single, inspectable system, the node makes visible what is normally abstracted away by large grids and markets.

What happens at this scale is not a special case — it is the same allocation problem faced by households, farms, factories, and entire economies. 

The D-NODE simply makes the choices explicit.


Here is a clear, non-technical, structurally tight explanation of the Load Classes, suitable to drop directly after the introduction in D_NODE.md. It keeps the focus on allocation logic, not hardware minutiae.


---

## Load Classes

The D-NODE organizes all energy use into three distinct load classes. These classes are not defined by technology, but by priority, flexibility, and time sensitivity. Every unit of energy entering the node must flow into one of these classes or be stored for later use. The separation makes allocation decisions explicit and auditable.

### 1. Domestic Load — Reliability-Critical

Domestic load represents essential, time-dependent energy use that cannot be deferred without loss of welfare. In the demo node, this load models basic household needs such as lighting and background appliance use. These loads exist regardless of solar conditions and are poorly aligned with peak generation.

Domestic load has the highest priority in the system. It must always be served first. If insufficient energy is available, the system has failed its primary responsibility. This load therefore defines the minimum reliability requirement of the microgrid and sets a hard lower bound on allocation decisions.

Domestic energy is not optimized. It is protected.


### 2. Industrial Load — Productive and Schedulable

Industrial load represents energy used for productive work that can be shifted in time. In the demo, this includes on-farm processing and a small lunch-only restaurant, forming a closed-loop example of agricultural production and consumption.

Unlike domestic load, industrial processes can be planned to coincide with solar availability. Milling, mixing, extrusion, drying, and food service are intentionally scheduled around midday when solar output is highest. This load converts energy into durable economic value rather than immediate consumption.

Industrial load demonstrates that when production adapts to energy, overall system efficiency and resilience increase without additional infrastructure.


### 3. Flexible Load — Surplus Absorber

The flexible load represents fully controllable, non-essential consumption that exists to absorb excess energy when all higher-priority needs are met. In the demo node, this role is fulfilled by an ASIC mining load, but the function is generic and interchangeable.

This load has the lowest priority and is only engaged when:

- Domestic load is fully supplied

- Industrial load is running as scheduled

- Storage is charging or full


The flexible load can be switched, stepped, or throttled in real time to match available surplus. Its purpose is not to drive the system, but to prevent curtailment and wasted generation.

---

## Load Priority and Allocation Logic

The three load classes form a simple hierarchy:

1. **Domestic** - must always be served


2. **Industrial** - served when energy is available


3. **Flexible** - served only if energy would otherwise be unused


This hierarchy allows the node to:

- Remain stable under variable generation

- Maximize renewable utilization

- Demonstrate demand-side management without complexity


The key insight is that flexibility, not storage alone, enables high renewable penetration. The D-NODE makes this visible in hardware.

---

## System Overview

This diagram (link) shows the architecture of the D-NODE off-grid solar microgrid demo, designed to illustrate how domestic, industrial, and flexible loads can be balanced using photovoltaic generation and demand-side control. 

Six PV panels feed a Victron MPPT, charging a 48 V LiFePO₄ battery and supplying AC loads via an inverter/charger, with clear separation between DC power flows and AC distribution.

Load control is managed by Home Assistant via Zigbee relays, using time-of-day scheduling and PV availability. 

Domestic loads (priority 1) are always supplied, industrial loads for on-farm pasta production and a lunch-only restaurant (priority 2) are scheduled to align with midday solar generation, and a flexible ASIC load (priority 3) is enabled only when surplus PV energy is available to avoid curtailment. 

The battery provides buffering for night and morning demand, while system status and energy flows are monitored through the Victron Cerbo GX.

---

## Midday Balance Snapshot

Midday is the most important teaching moment in the D-NODE because it reveals how allocation, not generation determines system performance.

At peak solar, the demo array produces approximately 2.4 kW. Rather than curtailing excess power or overcharging batteries, the node distributes this energy across all three load classes in priority order.

## Energy Flows at Midday

Load Class /	Power / Allocation Rationale

Domestic	~0.24 kW	Always-on, reliability-critical demand

Industrial	~1.0 kW	Scheduled production aligned with PV peak

Flexible (ASIC)	~1.1–1.2 kW	Absorbs remaining surplus

Total	≈ 2.4 kW	Full utilization of generation


## What This Demonstrates

**No curtailment**
All available solar energy is used productively.

**No battery stress**
Batteries are neither forced to absorb excess power nor cycled unnecessarily.

**Stable voltage and frequency**
Load follows generation instead of fighting it.

**Clear allocation logic**
Energy is not “consumed” randomly, it is assigned deliberately.


This snapshot makes visible a core principle of Allocation Economics:
scarcity is not eliminated by overbuilding supply, but by allocating demand intelligently.


---

## Flexible Loads and Why They Matter

Flexible loads are the final layer of the allocation stack. They exist to absorb energy that would otherwise be wasted once all higher-priority needs are met.

In the D-NODE, this role is fulfilled by an ASIC mining load—not because it is unique, but because it is functionally ideal.

---

## Why ASICs Are the Perfect Flexible Load

ASICs have a rare combination of properties that make them exceptionally well-suited for this role:

**Fully dispatchable**
They can be turned on, off, or throttled instantly without damage or efficiency loss.

**Location-independent**
They require no proximity to users, markets, or infrastructure beyond power and connectivity.

**Elastic consumption**
They scale smoothly from watts to kilowatts, matching surplus precisely.

**Non-essential by design**
No harm occurs if they stop. This makes them safe to deprioritize.

In allocation terms, ASICs have zero entitlement. They consume only what remains.


---

## Dual Outputs: Heat and Bitcoin

Unlike most surplus sinks, ASICs produce two outputs—both of which add value.

### 1. Heat (Immediate, Local)

All electrical energy consumed by an ASIC is converted into heat. In real deployments, this heat can be:

- Recovered for space heating

- Used for water heating or drying

- Integrated into agricultural or industrial processes


Even in the demo, the heat serves as a visible reminder that no energy disappears, it only changes form.

### 2. Bitcoin (Abstract, Durable)

Bitcoin represents the opportunity value of surplus energy:

- It is stored without decay

- It is transferrable across time and geography

- It requires no intermediary

Importantly, Bitcoin is not required for the node to function.
The microgrid operates perfectly without it.

Bitcoin exists only to answer one question:

```
> What should we do with energy that would otherwise be wasted?

```


## Flexible Loads as a Design Principle

ASIC computers mining Bitcoin are not the only example of a flexible load. The same role could be filled by:

- Data processing

- Desalination

- Electrolysis

- Cold storage

- Material preprocessing


What matters is not the technology, but the allocation behavior.

The D-NODE shows that when flexible demand exists, renewable systems stop needing excuses for waste.

They simply allocate.






