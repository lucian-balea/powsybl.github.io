---
title: load-flow-action-simulator
layout: default
todo:
    - add a link to http://rte-france.github.io/hades2/index.html
    - the debug property seems unused
---

The `load-flow-action-simulator` module is used by the [action-simulator](../../tools/action-simulator.md) tool if it's
configured to use the `LoadFlowActionSimulator` implementation.

# Properties

## copy-strategy
Use the `copy-strategy` to define how the action-simulator will store and restore network state internally. This choice
can greatly impact performances.
Possible values are:
- STATE: will only save and restore state data. Optimizes performances, but will not behave correctly if some actions
modify the structure of the network.
- DEEP: will save and restore all network data. Decreases performances, but allows to use any type of action.

## ignore-pre-contingency-violations
Set the `ignore-pre-contingency-violations` to `true` to ignore the pre-contingency violations and continue the
simulation even if there are still violations after the pre-contingency simulation.

## load-flow-name
The `load-flow-name` property is an optional property that defines the implementation name to use for running the loadflow. 
If this property is not set, the default loadflow implementation is used. See [Loadflow Configuration](load-flow.md) to configure the default loadflow.
**Note**: In previous Powsybl releases (before 3.0.0), this was configured in the `load-flow-factory` property with the full classname of the implementation.

## max-iterations
Use the `max-iterations` parameter to limit the number of iteration needed to solve the violations.

# Examples

## YAML
```yaml
load-flow-action-simulator:
    copy-strategy: STATE
    debug: false
    ignore-pre-contingency-violations: false
    load-flow-name: Mock
    max-iterations: 10
```

## XML
```xml
<load-flow-action-simulator>
    <copy-strategy>STATE</copy-strategy>
    <debug>false</debug>
    <ignore-pre-contingency-violations>false</ignore-pre-contingency-violations>
    <load-flow-name>Mock</load-flow-name>
    <max-iterations>10</max-iterations>
</load-flow-action-simulator>
```
