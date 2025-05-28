# Arm CMSIS Solution

The Arm® CMSIS Solution extension is a graphical user interface for csolution projects that use the [CMSIS-Toolbox](https://open-cmsis-pack.github.io/cmsis-toolbox/). The extension supports microcontroller devices that incorporate Arm Cortex®-M processors and Arm Ethos®-U Neural Processing Units (NPUs), and works with various C/C++ compilers and debuggers. 

This extension is [free to use](https://marketplace.visualstudio.com/items/Arm.cmsis-csolution/license) and you can install it individually or as part of the [Arm Keil® Studio Pack](https://marketplace.visualstudio.com/items?itemName=Arm.keil-studio-pack).

Arm CMSIS Solution provides the following views:

- [CMSIS view](#cmsis-view): Access your source code and actions such as build, run, and debug from the **Solution outline**.
- [Create Solution view](#create-solution-view): Create new solutions for devices or boards from template projects or example applications.
- [Configure Solution view](#configure-solution-view): Add layers to your reference applications or select a compiler toolchain for your solutions.
- [Manage Solution view](#manage-solution-view): Manage your solutions with multiple targets, projects, and build types to define the scope of your applications.
- [Software Components view](#software-components-view): Access reusable building blocks that are provided in software packs.

[Settings](https://mdk-packs.github.io/vscode-cmsis-solution-docs/configuration.html#configure-the-extension): Configure features like pack download, [clangd](https://marketplace.visualstudio.com/items?itemName=llvm-vs-code-extensions.vscode-clangd), or usage of web services. When **Use Web Services** is enabled, Arm CMSIS Solution gets from [keil.arm.com](https://www.keil.arm.com/packs/) information about devices, boards, and examples that are provided in software packs.

Arm CMSIS Solution works as a standalone tool and can also interact with other VS Code extensions:

- [Arm Tools Environment Manager](https://marketplace.visualstudio.com/items?itemName=Arm.environment-manager): Installs tools (compiler, debugger, simulation models, and utilities) for software development.
- [Arm CMSIS Debugger](https://marketplace.visualstudio.com/items?itemName=Arm.vscode-cmsis-debugger): Installs a GDB-based debugger (for CMSIS-DAP, ULINK, JLink, ST-Link, an other adapters) along with [pyOCD](https://pyocd.io/).
- [Red Hat YAML](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml): Provides syntax support when editing csolution project files such as `*.csolution.yml` and `*.cproject.yml`.
- [clangd](https://marketplace.visualstudio.com/items?itemName=llvm-vs-code-extensions.vscode-clangd): Adds smart features to the VS Code editor, including code completion, compile errors, and go-to-definition.

## Feature overview

![CMSIS Solution Quick Tutorial](./docs/videos/MDK6_Productivity.gif)

For detailed information refer to [User Interface](https://mdk-packs.github.io/vscode-cmsis-solution-docs/userinterface.html) in the CMSIS Solution documentation.

## CMSIS view

The **CMSIS** view gives you access to the source code of your application. The **CMSIS** view shows the [multiple projects](https://open-cmsis-pack.github.io/cmsis-toolbox/build-overview/#project-setup-for-related-projects) that belong to the context set. The various elements available for a project are:

- [Board](https://open-cmsis-pack.github.io/cmsis-toolbox/YML-Input-Format/#board): The name of the target board and documentation.
- [Device](https://open-cmsis-pack.github.io/cmsis-toolbox/YML-Input-Format/#device): The name of the target device, documentation, and device-specific debug options (`*.dbgconf`).
- [File groups](https://open-cmsis-pack.github.io/cmsis-toolbox/YML-Input-Format/#groups): Groups used to organize user source code.
- [Constructed-files](https://open-cmsis-pack.github.io/cmsis-toolbox/build-overview/#rte_componentsh): Files generated for the CMSIS Run-Time Environment (RTE).
- [Linker](https://open-cmsis-pack.github.io/cmsis-toolbox/build-overview/#linker-script-management): Script files used in the project context and access to linker map file.
- [Components](https://open-cmsis-pack.github.io/cmsis-toolbox/CreateApplications/#software-components): Reusable software modules that you select in the [Software Components view](#software-components-view). You can also access documentation or a run configuration generator such as [STM32CubeMX](https://open-cmsis-pack.github.io/cmsis-toolbox/CubeMX/) or [MCUXpresso Config](https://open-cmsis-pack.github.io/cmsis-toolbox/MCUXpressoConfig/).
- [Layers](https://open-cmsis-pack.github.io/cmsis-toolbox/build-overview/#software-layers): Sets of source files, software components, and configuration files that you can reuse in different projects.

Action buttons allow you to build, run, and debug your application, [edit *csolution project files*](#yml-editor-support) or [manage the solution configuration](#manage-solution-view). The [Configuration Wizard](#configuration-wizard) offers a graphical view to configuration file options.

## Create Solution view

![Create Solution](https://github.com/ARM-software/vscode-cmsis-csolution/raw/main/docs/images/CreateNewSolution.png)

To start a new *csolution project*, select a [board](https://www.keil.arm.com/boards/) or [device](https://www.keil.arm.com/devices/) and choose from the following project types:

- Templates: Templates are stub projects providing a minimal setup for the selected use case.
- [Reference applications](https://open-cmsis-pack.github.io/cmsis-toolbox/ReferenceApplications/): Reference applications are hardware-agnostic and require additional software layers with API drivers for the target board selected.
- CMSIS solution examples: These examples are created for a specific hardware or evaluation board and interface with board and device peripherals.
- µVision examples: Example projects created for the µVision IDE. Arm CMSIS Solution automatically converts µVision projects to the csolution project format.

Then create the *csolution project* on the selected folder on your Host computer.

## Configure Solution view

![Configure Solution](https://github.com/ARM-software/vscode-cmsis-csolution/raw/main/docs/images/ConfigureSolution.png)

When using a [reference application](https://open-cmsis-pack.github.io/cmsis-toolbox/ReferenceApplications/) select compatible software layers for your solution from this view.

## Software Components view

![Software Components](https://github.com/ARM-software/vscode-cmsis-csolution/raw/main/docs/images/SoftwareComponents.png)

Select reusable software components for your application from this view.

[CMSIS-Packs](https://open-cmsis-pack.github.io/Open-CMSIS-Pack-Spec/main/html/index.html) provide software components with other optional items such as configuration files, documentation, and user code templates. A software component typically interfaces with other software components or with device peripherals. The list of software components depends on the device or board selected.

## Manage Solution view

![Manage Solution](https://github.com/ARM-software/vscode-cmsis-csolution/raw/main/docs/images/ManageSolution.png)

Select a [context set](https://open-cmsis-pack.github.io/cmsis-toolbox/build-overview/#working-with-context-set) from this view. For a given target type, a context set combines related projects which you can build for an application. You might need to use different build types for projects, for example in cases where not all parts of an application require extra debug overhead.

## Configuration Wizard

![Configuration Wizard](https://github.com/ARM-software/vscode-cmsis-csolution/raw/main/docs/images/ConfigWizard.png)

Many configuration files have annotations for the [CMSIS Configuration Wizard](https://open-cmsis-pack.github.io/Open-CMSIS-Pack-Spec/main/html/configWizard.html). Using the **Open Preview** button in the editor allows you to modify options in a graphical view.

## YML Editor Support

![YML Editor Support](https://github.com/ARM-software/vscode-cmsis-csolution/raw/main/docs/images/SyntaxYML.png)

The YML syntax support in the editor detects errors, provides auto completion, and documentation links on hover over.

## Run and Debug

Arm CMSIS Solution generates the [Run and Debug configuration](https://mdk-packs.github.io/vscode-cmsis-solution-docs/conf_debug.html) files (`launch.json` and `tasks.json`) for the [Arm CMSIS Debugger](https://marketplace.visualstudio.com/items?itemName=Arm.vscode-cmsis-debugger) and [pyOCD](https://pyocd.io/). It supports single-core and multi-core configurations for CMSIS-DAP, ULINK, JLink, and ST-Link debug adapters.

The [Run and Debug configuration](https://mdk-packs.github.io/vscode-cmsis-solution-docs/configuration.html#configure-run-and-debug) is enabled with the `target-set:` node and a `debugger:` setting as shown below:

```yml
  target-types:
    - type: FRDM-K32L3A6
      board: FRDM-K32L3A6
      device: K32L3A60VPJ1A
      target-set:
        - set:
          debugger:
            name: CMSIS-DAP
            interface: swd
```

## Related

- [CMSIS Solution for VS Code Documentation](https://mdk-packs.github.io/vscode-cmsis-solution-docs/)
- [Available Software Packs](https://www.keil.arm.com/packs/)

## Submit feedback or report issues

To submit feedback or report issues on the Arm CMSIS Solution extension, please use [GitHub issues](https://github.com/ARM-software/vscode-cmsis-csolution/issues) in the extension repository.
