# Arm CMSIS Solution

The Arm® CMSIS Solution extension is a graphical user interface for csolution projects that use the [CMSIS-Toolbox](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/README.md). It supports microcontroller devices that incorporate Arm Cortex®-M processors and Arm Ethos®-U Neural Processing Units (NPUs), and works with various C/C++ compilers and debuggers. This extension is [free to use](https://marketplace.visualstudio.com/items/Arm.cmsis-csolution/license) and you can install it individually or as part of the [Arm Keil Studio Pack](https://marketplace.visualstudio.com/items?itemName=Arm.keil-studio-pack).

The complete [documentation](https://developer.arm.com/documentation/108029/latest/Extension-pack-and-extensions) for Arm CMSIS Solution and the other Keil® Studio extensions is available on Arm Developer.

Arm CMSIS Solution provides the following views:

- [CMSIS view](#cmsis-view): Access your source code and actions such as build, run, and debug from the **Solution outline**.
- [Create New Solution view](#create-new-solution-view): Create new solutions for devices or boards from template projects or example applications.
- [Configure Solution view](#configure-solution-view): Add layers to your reference applications or select a compiler toolchain for your solutions.
- [Manage Solution view](#manage-solution-view): Manage your solutions with multiple targets, projects, and build types to define the scope of your application programs.
- [Software Components view](#software-components-view): Access reusable building blocks that are provided in software packs.

[Settings](https://code.visualstudio.com/docs/getstarted/settings#_extension-settings): Configure features like [clangd](https://marketplace.visualstudio.com/items?itemName=llvm-vs-code-extensions.vscode-clangd). With the **Online Mode** setting, Arm CMSIS Solution uses web services to retrieve information about devices, boards, and examples, and downloads missing **software packs**.

Arm CMSIS Solution works as a standalone tool and can also interact with other Visual Studio Code extensions:

- [Arm Environment Manager](https://marketplace.visualstudio.com/items?itemName=Arm.environment-manager): Installs tools (compiler, debugger, simulation models, and utilities) for software development.
- [Red Hat YAML](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml): Provides syntax support when editing csolution project files such as `*.csolution.yml` and `*.cproject.yml`.
- [clangd](https://marketplace.visualstudio.com/items?itemName=llvm-vs-code-extensions.vscode-clangd): Adds smart features to the Visual Studio Code editor, including code completion, compile errors, and go-to-definition.

Arm CMSIS Solution interfaces with the following [debug](#run-and-debug) extensions:

- [Arm Debugger](#arm-debugger): Supports connections to physical targets such as ULINK, CMSIS-DAP, and ST-LINK, and virtual targets (FVP simulation models).
- [Cortex-Debug](#cortex-debug): Interfaces with physical targets using J-Link, OpenOCD, pyOCD, or ST-LINK. OpenOCD and pyOCD support debug with CMSIS-DAP.

## CMSIS view

![CMSIS view](https://github.com/ARM-software/vscode-cmsis-csolution/raw/main/docs/images/CMSIS_View.png)

The **CMSIS** view gives you access to the source code of your application. The **CMSIS** view shows the [multiple projects](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/build-overview.md#project-setup-for-related-projects) that belong to the **context-set**, also called the build context. The various elements available for a project are:

- [File groups](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/YML-Input-Format.md#groups): Groups used to organize user source code.
- [Constructed-files](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/build-overview.md#rte_componentsh): Files generated for the CMSIS Run-Time Environment (RTE).
- [Linker](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/build-overview.md#linker-script-management): Script files used in the project context.
- [Components](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/CreateApplications.md#software-component): Reusable software modules that you select.
- [Layers](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/build-overview.md#software-layers): Sets of source files, software components, and configuration files that you can reuse in different projects.

Action buttons allow you to build, run, and debug your application or open the views that are described in detail below. For components, you can access the documentation or run generators such as STM32CubeMX or the MCUXpresso Config Tools.

## Create New Solution view

![Create New Solution](https://github.com/ARM-software/vscode-cmsis-csolution/raw/main/docs/images/CreateNewSolution.png)

Create a new csolution project and choose the target type name, solution name, and location of the csolution project from this view.

To start a new csolution project, select a [board](https://www.keil.arm.com/boards/) or [device](https://www.keil.arm.com/devices/). You can choose from the following project types:

- Templates: Templates are stub projects providing a minimal setup for the selected use case.
- [Reference applications](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/ReferenceApplications.md): Reference applications are hardware-agnostic and require additional software layers with API drivers for the target board selected.
- CMSIS solution examples: These examples are created for a specific hardware or evaluation board and interface with board and device peripherals.
- µVision examples: Example projects created for the µVision IDE. Arm CMSIS Solution automatically converts µVision projects to the csolution project format.

## Configure Solution view

![Configure Solution](https://github.com/ARM-software/vscode-cmsis-csolution/raw/main/docs/images/ConfigureSolution.png)

Select software layers and a compiler toolchain for your solution from this view.

## Software Components view

![Software Components](https://github.com/ARM-software/vscode-cmsis-csolution/raw/main/docs/images/SoftwareComponents.png)

Select reusable software components for your application from this view.

[CMSIS-Packs](https://open-cmsis-pack.github.io/Open-CMSIS-Pack-Spec/main/html/index.html) provide software components with other optional items such as configuration files, documentation, and user code templates. A software component typically interfaces with other software components or with device peripherals. The list of software components depends on the device or board selected.

## Manage Solution view

![ManageSolution](https://github.com/ARM-software/vscode-cmsis-csolution/raw/main/docs/images/ManageSolution.png)

Select a [context-set](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/build-overview.md#working-with-context-set), or build context, from this view. A build context combines related projects which are generated independently for an application program. You might need to use different build types for projects, for example in cases where not all parts of an application require extra debug overhead.

## Run and Debug

Arm CMSIS Solution uses standard Visual Studio Code [task configurations](https://code.visualstudio.com/docs/editor/tasks) to configure the **Run** action (`tasks.json`) and [launch configurations](https://code.visualstudio.com/docs/editor/debugging#_launch-configurations) to configure the **Debug** action (`launch.json`). The `tasks.json` and `launch.json` files are located in the `.vscode` folder of your workspace (the csolution project root folder). These files store settings that you can select from the **Run Configuration** and **Debug Configuration** editors or add manually in the `tasks.json` and `launch.json` files.

![Run and Debug](https://github.com/ARM-software/vscode-cmsis-csolution/raw/main/docs/images/RunDebug.png)

### Arm Debugger

The [Arm Debugger](https://marketplace.visualstudio.com/items?itemName=Arm.arm-debugger) extension supports connections to physical targets such as ULINK, CMSIS-DAP, and ST-LINK, and virtual targets (FVP simulation models).

Refer to the [Arm Debugger extension documentation](https://developer.arm.com/documentation/108029/latest/Arm-Debugger-extension) for more details.

### Cortex-Debug

The [Cortex-Debug](https://marketplace.visualstudio.com/items?itemName=marus25.cortex-debug) extension interfaces with J-Link, OpenOCD, pyOCD, or ST-LINK. OpenOCD and pyOCD support debug units with CMSIS-DAP firmware. Cortex-Debug requires the [GCC Toolchain for ARM CPUs](https://www.keil.arm.com/artifacts/#compilers/arm/arm-none-eabi-gcc) and the executables must be registered in the PATH environment variable of the host PC. For more information, refer to the [Cortex-Debug documentation](https://github.com/Marus/cortex-debug/wiki).

#### Interface with J-Link

To install the [J-Link Software Pack](https://www.segger.com/downloads/jlink/#J-LinkSoftwareAndDocumentationPack) and configure Cortex-Debug, use the following steps:

1. Use the `Debug: Add Configuration...` command from the Command Palette and select `Cortex Debug: JLink` to add the J-Link debug configuration to the `launch.json` file.

2. Update the debug configuration in the `launch.json` file to reflect your setup. For example:

    ```json
        {
            "cwd": "${workspaceFolder}",
            "executable": "${command:cmsis-csolution.getBinaryFiles}",
            "name": "Debug with JLink",
            "request": "launch",
            "type": "cortex-debug",
            "device": "${command:cmsis-csolution.getDeviceName}",
            "runToEntryPoint": "main",
            "showDevDebugOutput": "none",
            "servertype": "jlink",
            "serverpath": "<path>/JLinkGDBServerCL.exe"
        }
    ```

**Note:** `serverpath` is the path to the installed J-Link GDB server.

For more information, refer to the [J-Link Visual Studio Code documentation](https://wiki.segger.com/J-Link_Visual_Studio_Code).

#### Interface with OpenOCD

Install [OpenOCD](https://openocd.org/) and check that it is registered in the PATH environment variable of the host PC.

To configure Cortex-Debug for OpenOCD, use the following steps:

1. Use the `Debug: Add Configuration...` command from the Command Palette and select `Cortex Debug: OpenOCD` to add the OpenOCD debug configuration to the `launch.json` file.

2. Update the debug configuration in `launch.json` file to reflect your setup. For example:

    ```json
        {
            "cwd": "${workspaceRoot}",
            "executable": "${command:cmsis-csolution.getBinaryFiles}",
            "name": "Debug with OpenOCD",
            "request": "launch",
            "type": "cortex-debug",
            "servertype": "openocd",
            "configFiles": [ "openocd.cfg" ],
            "searchDir": [],
            "runToEntryPoint": "main",
            "showDevDebugOutput": "none"
        }
    ```

3. Create a configuration file named `openocd.cfg` in your workspace (in the csolution project root folder) and specify either `interface` and `target`, or `board` (which typically imports the `interface` and `target`).

**Examples:**

```txt
# interface: Debug Adapter CMSIS-DAP
source [find interface/cmsis-dap.cfg]

# target: Device STM32L4xx
source [find target/stm32l4x.cfg]
```

```txt
# board: STM32L4R9I-DISCO with ST-LINK
source [find board/stm32l4r9i-disco.cfg]
```

#### Interface with pyOCD

To install [pyOCD](https://pyocd.io/) and configure Cortex-Debug, use the following steps:

1. Use the `Debug: Add Configuration...` command from the Command Palette and select `Cortex Debug: PyOCD` to add the pyOCD debug configuration to the `launch.json` file.

2. Update the debug configuration in the `launch.json` file to reflect your setup. For example:

    ```json
        {
            "cwd": "${workspaceRoot}",
            "executable": "${command:cmsis-csolution.getBinaryFiles}",
            "name": "Debug with PyOCD",
            "request": "launch",
            "type": "cortex-debug",
            "targetId": "stm32l475xc",
            "runToEntryPoint": "main",
            "showDevDebugOutput": "none",
            "servertype": "pyocd"
        }
    ```

**Notes:**

- `targetId` is the target identifier if the target is not detected automatically.
- If there are multiple debug probes available, select the debug adapter you need when pyOCD is launched.

#### Interface with ST-LINK

Install [STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html) that includes the ST-LINK GDB server, then configure Cortex-Debug with the following steps:

1. Use the `Debug: Add Configuration...` command from the Command Palette and select `Cortex Debug: ST-LINK` to add the ST-LINK debug configuration to the `launch.json` file.

2. Update the debug configuration in the `launch.json` file to reflect your setup. For example:

    ```json
        {
            "cwd": "${workspaceRoot}",
            "executable": "${command:cmsis-csolution.getBinaryFiles}",
            "name": "Debug with ST-Link",
            "request": "launch",
            "type": "cortex-debug",
            "runToEntryPoint": "main",
            "showDevDebugOutput": "none",
            "servertype": "stlink"
        }
    ```

## Submit feedback or report issues

To submit feedback or report issues on the Arm CMSIS Solution extension, please use [GitHub issues](https://github.com/ARM-software/vscode-cmsis-csolution/issues) in the extension repository.
