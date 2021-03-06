---
title: Internal data model
layout: default
---

Powsybl's internal data model describes electrical networks via [a network core model](#network-core-model) which represents the network equipments
and its main attributes and [network extensions](#network-extensions) which can specify equipments' particular attributes for custom use cases.

# Network core model

The [Network](network.md) core modeling is made of two main objects: substations and lines. A substation can have several voltage levels and a line can be of several types:

- [Line](line.md) to model AC lines;
- [HVDC line](hvdcLine.md) to model DC lines;
- [Tie line](tieLine.md) to model a AC line segment shared between two countries;

- A [Substation](substation.md) can be made of several voltage levels, which are connected through transformers:

    - [Two windings transformer](twoWindingsTransformer.md)

    - [Three windings transformer](threeWindingsTransformer.md)

    - [VoltageLevel](voltageLevel.md)
        - [Node/Breaker topology](../../todo.md)
        - [Bus/Breaker topology](../../todo.md)
        - [Battery](battery.md)
        - [Generator](generator.md)
        - [Load](load.md)
        - [Shunt compensator](shuntCompensator.md)
        - [Dangling line](danglingLine.md)
        - [Static VAR compensator](staticVarCompensator.md)
        - [AC/DC converter station](hvdcConverterStation.md)

The following image shows some elements of the internal data model:

![IIDM model](./images/schema-iidm.png){: width="70%" .center-image}

IIDM format and its serialization/deserialization have several versions.
This page documents the latest IIDM version, available on latest `SNAPSHOT` version.

For more information on prior versions, [`powsybl-core`'s wiki page](https://github.com/powsybl/powsybl-core/wiki) lists
all the format's evolutions for each version.

# Network extensions

As explained above, network extensions can describe electrical equipments' attributes which are only useful for some
specific use cases (e.g. dynamic simulation, UCTE networks merging, etc.). The following extensions are provided by
Powsybl framework:

- ActivePowerControl for [generators](generator.md#active-power-control) and [batteries](battery.md#active-power-control)
- [CgmesConversionContextExtension](../../todo.md)
- [CgmesModelExtension](../../todo.md)
- [CoordinatedReactiveControl](../../todo.md)
- [Entsoe Area](../../todo.md)
- [MergedXnode](../../todo.md)
- [ThreeWindingsTransformerPhaseAngleClock](../../todo.md)
- [TwoWindingsTransformerPhaseAngleClock](../../todo.md)
- [Xnode](../../todo.md)

However, it is also possible to [create you own custom network extension for your need](../../todo.md).
