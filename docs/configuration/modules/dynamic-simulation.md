---
title: dynamic-simulation
layout: default
---

The `dynamic-simulation` module is used to configure the dynamic simulation default implementation name. Each dynamic simulation implementation provides a subclass of `com.powsybl.dynamicsimulation.DynamicSimulationProvider` correctly configured to be found by `java.util.ServiceLoader`. A dynamic simulation provider exposes a name that can be used in the dynamic simulation Java API to find a specific dynamic simulation implementation. It can also be used to specify a default implementation in this platform config module. If only one `com.powsybl.dynamicsimulation.DynamicSimulationProvider` is present in the classpath, there is no need to specify a default dynamic simulation implementation name. In the case where more than one `com.powsybl.dynamicsimulation.DynamicSimulationProvider` is present in the classpath, specifying the default implementation name allows dynamic simulation API user to use DynamicSimulation.run(...) and  DynamicSimulation.runAsync(...) methods to run a dynamic simulation. Using these methods when no default dynamic simulation name is configured and multiple implementations are in the classpath will throw an exception. An exception is also thrown if no implementation at all is present in the classpath, or if specifying a dynamic simulation name that is not present on the classpath.

# Properties

## default
Use the `default` property to specify the name of the default dynamic simulation implementation.

# Examples

## YAML
```yaml
dynamic-simulation:
    default: Mock
```

## XML
```xml
<dynamic-simulation>
    <default>Mock</default>
</dynamic-simulation>
```