---
title: dynamic-simulation
layout: default
---

The `dynamic-simulation` command is used to run dynamic simulations on the network.

# Usage
```shell
$> itools dynamic-simulation --help
usage: itools [OPTIONS] dynamic-simulation --case-file <FILE> [--help] [-I <property=value>]
              [--import-parameters <IMPORT_PARAMETERS>] [--output-file <FILE>]
              [--parameters-file <FILE>] [--skip-postproc]

Available options are:
    --config-name <CONFIG_NAME>   Override configuration file name

Available arguments are:
    --case-file <FILE>                            the case path
    --help                                        display the help and quit
-I <property=value>                               use value for given importer
                                                  parameter
    --import-parameters <IMPORT_PARAMETERS>       the importer configuation file
    --output-file <FILE>                          dynamic simulation results output path
    --parameters-file <FILE>                      dynamic simulation parameters as JSON file
    --skip-postproc                               skip network importer post
                                                  processors (when configured)

```

## Required parameters

### case-file
Use the `--case-file` parameter to specify the path of the case file.

## Optional parameters

### import-parameters
Use the `--import-parameters` parameter to specify the path of the configuration file of the importer. It is possible to
overload one or many parameters using the `-I property=value` parameter. The properties depend on the input format.
Refer to the documentation page of each [importer](../iidm/importer/index.md) to know their specific configuration.

### output-file
Use the `--output-file` parameter to export the result of the computation to the specified path. If this parameter is not
used, the results are printed to the console.

### parameters-file
Use the `--parameters-file` parameter to specify a JSON configuration file. If this parameter is not set, the default
configuration is used.

### skip-postproc
Use the `--skip-postproc` parameter to skip the importer's post processors. Read the [post processor](../iidm/importer/post-processor/index.md)
documentation page to learn more about importer's post processors.

# Configuration
To run a dynamic simulation, one has to choose the implementation, follow the instructions at [dynamic simulation Configuration](../configuration/modules/dynamic-simulation.md).

To set the default configuration of the dynamic simulation, one has to configure the
[dynamic-simulation-default-parameters](../configuration/modules/dynamic-simulation-default-parameters.md) module.

To learn more about configuration files, read the [DynamicSimulationParameters](../configuration/parameters/DynamicSimulationParameters.md) documentation
page.

# Examples
The following example shows how to run a dynamic simulation, using the default configuration:
```shell
$> itools dynamic-simulation --case-file case.xiidm
Loading network 'case.xiidm'
dynamic simulation results:
+--------+
| Result |
+--------+
| true   |
+--------+
```

The following example shows how to run a dynamic simulation using a parameters file:
```shell
$> itools dynamic-simulation --case-file case.xiidm --parameters-file dynamicsimulationparameters.json
dynamic simulation results:
+--------+
| Result |
+--------+
| true   |
+--------+
```

# Maven configuration
To use the `dynamic-simulation` command, add the following dependencies to the `pom.xml` file:
```xml
<dependency>
    <groupId>com.powsybl</groupId>
    <artifactId>powsybl-dynamic-simulation-api</artifactId>
    <version>${powsybl.version}</version>
</dependency>
```
