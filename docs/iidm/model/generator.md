---
title: Generator
layout: default
---

The `com.powsybl.iidm.network.Generator` interface is used to model a generator. A generator is connected to the network through a terminal.

# Characteristics

| Attribute | Type | Unit | Required | Default value | Description |
| --------- | ---- | ---- | -------- | ------------- | ----------- |
| EnergySource | [`EnergySource`](#energysource) | - | yes | `OTHER` | The energy source |
| MinP | double | MW | yes | - | The minimal active power |
| MaxP | double | MW | yes | - | The maximum active power |
| RegulatingTerminal | [`Terminal`](terminal.md) | - | no | The generator's terminal | The terminal used for regulation |
| VoltageRegulatorOn | boolean | - | yes | - | The voltage regulator status |
| TargetP | double | MW | yes | - | The active power target |
| TargetQ | double | MVAr | only if `VoltageRegulatorOn` is set to `false` | - | The reactive power target |
| TargetV | double | kV | only if `VoltageRegulatorOn` is set to `true` | - | The voltage target |
| RatedS | double | MVA | yes | - | The rated nominal power |

## EnergySource
The `com.powsybl.iidm.network.EnergySource` enum contains these six values:
- HYDRO
- NUCLEAR
- WIND
- THERMAL
- SOLAR
- OTHER

## Active Limits
The minimal active power is expected to be lower than the maximal active power.

## Targets
The voltage target is required if the voltage regulator is on.
The reactive power target is required if the voltage regulator is off.

## Regulation
The regulating terminal can be local or remote.

## Reactive Limits
A set of reactive limits can be associated to a generator. All the reactive limits modelings available in the library are described [here](reactiveLimits.md).

# Flow sign convention
Target values for generators (TargetP and TargetQ) are seen as target values for injections.
- They follow the generator sign convention.
- A value of TargetP positive means an injection into the bus.
- A positive value for the TargetP and the TargetQ means a negative value at the corresponding terminal.

# Examples
This example shows how to create a new `Generator` in the network:
```java
Generator generator = network.getVoltageLevel("VL").newGenerator()
    .setId("GEN")
    .setNode(1)
    .setEnergySource(EnergySource.HYDRO)
    .setMinP(0.0)
    .setMaxP(70.0)
    .setVoltageRegulatorOn(false)
    .setTargetP(0.0)
    .setTargetV(0.0)
    .setTargetQ(0.0)
    .add();
```

# Extensions

## Active power control

This extension is used to configure the participation factor of the generator, typically in the case of a loaflow computation with distributed slack.

| Attribute | Type | Unit | Required | Default value | Description |
| --------- | ---- | ---- | -------- | ------------- | ----------- |
| participate | boolean | - | yes | - | The participation status|
| droop | double | None (repartition key) | yes | - | The participation factor |

Here is how to add an active power control extension to a generator:
```java
generator.newExtension(ActivePowerControlAdder.class).withParticipate(true).withDroop(4).add();
```

## Coordinated reactive control

Some generators can be coordinated to control reactive power in a point of the network. This extension is used to configure the percent of reactive coordinated control that comes from a generator.

| Attribute | Type | Unit | Required | Default value | Description |
| --------- | ---- | ---- | -------- | ------------- | ----------- |
| QPercent | percent [0-100] | - | yes | - | The reactive control percent of participation |

Here is how to add a coordinated reactive control extension to a generator:
```java
generator.newExtension(CoordinatedReactiveControlAdder.class).withQPercent(40).add();
```

Please note that the sum of the `qPercent` values of the generators coordinating a same point of the network must be 100.