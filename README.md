# Arm CMSIS csolution

## Overview

This extension provides support for working with CMSIS solutions (csolution).

This Readme explains how to set up your development environment to be able to work with CMSIS solutions in Visual Studio Code.

Once your environment is ready, you can clone a csolution example project and install the CMSIS-Packs required for the example, and then start working with your example.

Note that you can also convert a Keil MDK project in `.uvprojx` format to a csolution project from the **Arm CMSIS csolution** extension.

## Useful resources

The **Arm CMSIS csolution** extension works in combination with the **Arm Device Manager** (Identifier: `arm.device-manager`) and **Arm Embedded Debugger** (Identifier: `arm.embedded-debug`) extensions to flash csolution projects to a device and do debugging.

## Submit feedback

To submit feedback, please [create an issue](https://github.com/ARM-software/vscode-cmsis-csolution/issues/new/choose).

## Table of contents

1. [Set up your development environment](#set-up-your-development-environment)
    - [Install the tools](#install-the-tools)
    - [Initialize the cache for CMSIS-Packs](#initialize-the-cache-for-cmsis-packs)
    - [Install the Visual Studio Code extensions](#install-the-visual-studio-code-extensions)
1. [Work with a csolution example project](#work-with-a-csolution-example-project)
    - [Clone a csolution example project](#clone-a-csolution-example-project)
    - [Install the CMSIS-Packs required for the example](#install-the-cmsis-packs-required-for-the-example)
    - [Explore what you can do with the Arm CMSIS csolution extension](#explore-what-you-can-do-with-the-arm-cmsis-csolution-extension)
    - [Convert a Keil MDK project to a csolution project](#convert-a-keil-mdk-project-to-a-csolution-project)

## Set up your development environment

Here are the main steps:

1. Install the following tools: compiler toolchain, CMake and Ninja and CMSIS-Toolbox.

1. Initialize the cache for CMSIS-Packs.

1. Install the Visual Studio Code extensions required to work with CMSIS solutions: **YAML Language Support by Red Hat**, **clangd**, **Arm Device Manager**, **Arm Embedded Debugger** and **Arm CMSIS csolution**.

### Install the tools

#### General comments

##### On macOS

Some unsigned binaries need to be de-quarantined before you can run them. This is only required for newer versions of macOS.

Run the command:

    ```
    xattr -d com.apple.quarantine /path/to/binary
    ```

Run with `sudo` if you get permission errors.

#####  On Windows

Use the **System Properties** dialog box to set environment variables and add directories to the PATH.

#### Install a compiler toolchain

Install the Arm Compiler for Embedded toolchain or the Arm GNU Toolchain (includes the GNU Compiler - GCC), or both.

##### Install the Arm Compiler for Embedded toolchain

On Windows or Linux, download Arm Compiler for Embedded from [Arm Developer](https://developer.arm.com/downloads/-/arm-compiler-for-embedded) or use the Arm Compiler for Embedded toolchain available with [Keil MDK](https://www2.keil.com/mdk5).

**Note**: There is no build available for macOS at the moment.

##### Install the Arm GNU Toolchain (GCC)

1. Download the latest Arm GNU Toolchain for your platform from
[Arm Developer](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/downloads). Choose the **arm-none-eabi** release for your platform.

    Archive files are available for all platforms. Installers are available for macOS and Windows.

1. Check the installation by running the following command:

        ```
        arm-none-eabi-g++ --help
        ```

#### Install CMake and Ninja

The CMSIS-Toolbox uses the CMake build system with a Ninja generator, so you must install these tools before installing CMSIS-Toolbox.

1. Install the CMake and Ninja build tools with your system package manager or download the latest releases from the CMake and Ninja download pages.

    - Installation with a system package manager:

      Example with Homebrew on macOS:

          ```
          brew install cmake
          brew install ninja
          ```

    - Installation from latest releases:

      - Download the CMake installer from here: https://cmake.org/download/
      - Download the Ninja executable from here: https://github.com/ninja-build/ninja/releases

1. If this has not already been handled by the system package manager, add `cmake` and `ninja` to the PATH.

1. Check the installation by running the following commands:

        ```
        cmake --version
        ninja --version
        ```

#### Install the CMSIS-Toolbox

1. Download the latest release of CMSIS-Toolbox for your platform from the
[Releases](https://github.com/Open-CMSIS-Pack/devtools/releases) page on GitHub.

    **Note**: There is no Apple silicon build available yet, but the **darwin64** version works with [Rosetta](https://developer.apple.com/documentation/apple-silicon/about-the-rosetta-translation-environment).

1. Extract the content of the archive file.

1. Modify the `*.cmake` file for the compiler toolchain you have installed. If you have several toolchains installed, modify the corresponding `*.cmake` files. All the `*.cmake` files are stored in `<cmsis-toolbox-installation-dir>/etc/`.

    Modify the section below:

        ```
        ############### EDIT BELOW ###############
        # Set base directory of toolchain
        set(TOOLCHAIN_ROOT "/home/runner/gcc-arm-none-eabi-10-2020-q4-major/bin")
        set(PREFIX arm-none-eabi-)
        set(EXT )
        ```

    Example:

        ```
        ############### EDIT BELOW ###############
        # Set base directory of toolchain
        set(TOOLCHAIN_ROOT "/Applications/ARM/bin")
        set(PREFIX arm-none-eabi-)
        set(EXT )
        ```

    **Notes**:
    - The exact toolchain version does not matter. For example, you can modify the `GCC.10.2.1.cmake` file if you have installed GCC 10.3.1.
    - `TOOLCHAIN_ROOT` should be set to the _absolute_ path to the compiler bin directory where the toolchain binaries are stored.
    - `EXT` gives the file extension of the executable binaries. Leave it empty for macOS and Linux. Use `.exe` for Windows.

1. Choose a location for storing CMSIS-Packs on your system. These are the defaults:

    - On Windows: `%LOCALAPPDATA%\Arm\Packs`
    - On macOS and Linux: `$HOME/.cache/arm/packs`

1. Set the following environment variables:

    - `CMSIS_COMPILER_ROOT`: Set to the path of the CMSIS-Toolbox `etc` directory. For example, `/<cmsis-toolbox-installation-dir>/etc`.
    - `PATH`: Add the CMSIS-Toolbox `bin` directory to the system path. For example, `/<cmsis-toolbox-installation-dir>/bin`.
    - `CMSIS_PACK_ROOT`: Set to the path of the CMSIS-Pack root directory that stores software packs. For example, `/open-cmsis/pack`. **Note**: Set this environment variable to an _absolute_ path, without variables or `~`.

1. On macOS:

    The CMSIS-Toolbox is currently not signed, so you must de-quarantine its binaries as explained in the [General comments](#general-comments) section.

    Run the command:

        ```
        xattr -d com.apple.quarantine <cmsis-toolbox-installation-dir>/bin/
        ```

    Run with `sudo` if you get permission errors.

1. Check the installation with:

        ```
        cbuild --version
        csolution --help
        ```

### Initialize the cache for CMSIS-Packs

Run the following command to initialize the cache:

    ```
    cpackget init https://www.keil.com/pack/index.pidx
    ```

### Install the Visual Studio Code extensions

#### Install the extensions

Open Visual Studio Code and install the extensions listed below from the **Extensions** view. You can search for extensions using their identifiers.

- **YAML Language Support by Red Hat** (Identifier: `redhat.vscode-yaml`): This extension provides IntelliSense support for csolution files.

- **clangd** (Identifier: `llvm-vs-code-extensions.vscode-clangd`): This extension provides IntelliSense support for C/C++ projects.

    **Note**: The extension requires the clangd language server. If the server is not found on your path, add it with the **clangd: Download language server** command from the Command Palette.

- **Arm Device Manager** (Identifier: `arm.device-manager`): This extension allows you to manage device connections for Arm Cortex-M based microcontrollers, development boards and debug probes.

- **Arm CMSIS csolution** (Identifier: `arm.cmsis-csolution`): This extension provides support for working with CMSIS solutions.

- **Arm Embedded Debugger** (Identifier: `arm.embedded-debug`): This extension allows you to do flashing and debugging on Arm Cortex-M based microcontrollers, development boards and debug probes implementing the Microsoft Debug Adapter Protocol (DAP).

#### Modify settings to point at CMSIS-Toolbox

Once you have installed the Arm CMSIS csolution extension, modify the extension settings to point at the tools installed previously.

1. In Visual Studio Code, go to **Code** > **Preferences** > **Settings**.

1. Find the **CMSIS csolution** extension under the **Extensions** category.

1. Set _absolute_ paths for:
    - The `cbuild` executable (available in the CMSIS-Toolbox **bin** directory) in the **Cbuild Path** field.
    - The `csolution` executable (available in the CMSIS-Toolbox **bin** directory) in the **Csolution Path** field.

1. Restart Visual Studio Code.

#### C/C++ language support with clangd

There is no extra setup needed once **clangd** has been installed. The **Arm CMSIS csolution** extension generates a `compile_commands.json` file for each project in a solution whenever a `.cprj` file changes or when you change the context of a solution (**Target** and **Build** types). A `.clangd` file is kept up to date for each project in the solution. The `.clangd` file is used by the **clangd** extension to locate the `compile_commands.json` files and enable IntelliSense. See the [clangd documentation](https://clangd.llvm.org/installation#project-setup) for more details.

You can turn off the automatic generation of the `.clangd` file and `compile_commands.json` file.

1. Go to **Code** > **Preferences** > **Settings**.

1. Find the **CMSIS csolution** extension under the **Extensions** category.

1. Clear the **Auto Generate Clangd File** and **Auto Generate Compile Commands** checkboxes.

## Work with a csolution example project

Now that your Visual Studio Code environment is set up, you can start working with a csolution project.

### Clone a csolution example project

Clone the following csolution example project from Visual Studio Code:

https://github.com/RobertRostohar/Demo_EW/tree/main/Blinky

### Install the CMSIS-Packs required for the example

1. Open the cloned example project from Visual Studio Code, then open the `Blinky.csolution.yml` file from the **Explorer** view.

    The required packs are listed under the `packs` key of the `csolution.yml` file.
    For example, for `Blinky.csolution.yml`, one of the required packs is `ARM::V2M_MPS3_SSE_300_BSP@1.2.0`, where `ARM` is the vendor, `V2M_MPS3_SSE_300_BSP` is the name of the pack, and `1.2.0` is the version.

1. Run the following command to add each pack:

      ```
      cpackget add <vendor>::<name>@<version>
      ```

### Explore what you can do with the Arm CMSIS csolution extension

In this example, we use the Blinky solution cloned previously. See [Clone a csolution example project](#clone-a-csolution-example-project).

1. Click the **CMSIS** icon ![CMSIS icon](./docs/images/cmsis-icon.png) in the Activity Bar to open the extension.

1. Look at the available contexts for the csolution. You can change the build target and build configuration.

    - **Active Solution**: The name of the csolution file `Blinky.csolution.yml`.
    - **Target**: The build target `B-U585I-IOT02A` (a physical evaluation board from STMicroelectronics) or `AVH_MPS3_Corstone-300` (a Virtual Hardware Target).
    - **Build**: The build configuration `Debug` or `Release`. A build configuration adds the flexibility to configure each build target towards a specific testing. Use `Debug` for a full debug build of the software for interactive debug, or `Release` for the final code deployment to the systems.
    - **Project**: The name of the cproject file `Blinky.cproject.yml`.

1. Click the **Explorer** icon ![Explorer icon](./docs/images/explorer-icon.png) and open the `Blinky.csolution.yml` and `Blinky.cproject.yml` files. YAML syntax support helps you with editing.

1. You will notice that when changes are made to the csolution or cproject files, the `.cprj` file is regenerated.

    1. Go to **View** > **Output**.

        The **OUTPUT** tab opens.

    1. Select **CMSIS Project Manager** in the drop-down list in the top right corner and check what has been logged.

1. Right-click on the `.cprj` file corresponding to the context you selected and select **Build**. Check the **TERMINAL** tab.

1. Open the `Blinky.c` file and check the IntelliSense features available.


**Note**: You can turn off the automatic generation of the `cprj` file.

  1. Go to **Code** > **Preferences** > **Settings**.

  1. Find the **CMSIS csolution** extension under the **Extensions** category.

  1. Clear the **Auto Generate Cprj** checkbox.

### Convert a Keil MDK project to a csolution project

You can convert a Keil MDK project to csolution project.

1. In Visual Studio Code, run the **CMSIS: Convert MDK project to csolution** command from the Command Palette.

1. Using the file picker that displays, select the `.uvprojx` that you want to convert and click **Select**.

    The conversion starts immediately.

1. Check the **OUTPUT** tab. Conversion messages are logged under the **MDK to csolution Converter** category.

    A "Conversion Successful" message displays once the conversion is done.
    The `*.cproject.yaml` and `*.csolution.yaml` files are available in the folder where the `.uvprojx` is stored.
