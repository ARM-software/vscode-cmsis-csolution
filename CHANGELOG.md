# Change Log

## [Unreleased]

## 1.58.1

- Solved issues:

  - The `CMSIS Context` status bar hangs at `Loading Solution...` during Solution load if a default `target-set` is not specified and no `cbuild-set.yml` with a context-set is present.
    [#304](https://github.com/ARM-software/vscode-cmsis-csolution/issues/304)

- Known issues:

  - Updating `launch.json` and `tasks.json` files does not preserve comments.

## 1.58.0

- New features:

  - [**CMSIS-View**](https://mdk-packs.github.io/vscode-cmsis-solution-docs/debug.html#cmsis-view) adds [PLM](https://open-cmsis-pack.github.io/cmsis-toolbox/build-overview/#plm-of-configuration-files)
    status indicators for component configuration files `(X)`= mandatory file update, `(!)` = recommended file update and `(?)` = suggested file update. These indicators are propagated upwards from
    the configuration file to the project displaying the most severe status. The tooltips to the status indicators provide additional information. When hovering over or selecting a configuration file
    that needs updating, a merge icon is displayed that can be clicked to open the [VSCode 3-way merge editor](https://code.visualstudio.com/docs/sourcecontrol/overview#_3way-merge-editor). When closing
    the editor the merged file becomes the active configuration file.

- Solved issues:

  - [**Configuration Wizard**] when editing a bitfield through the graphical view, no other bitfield values get incorrectly reset. [#296](https://github.com/ARM-software/vscode-cmsis-csolution/issues/296)
  - Removed unintended duplicates of directories from some examples projects downloaded from the Web (<https://Keil.arm.com>). [#99](https://github.com/ARM-software/vscode-cmsis-csolution/issues/99)
  - The generation of `launch.json` and `task.json` do not rewrite the files unless updates are required. This way comments are preserved when not making changes. [#295](https://github.com/ARM-software/vscode-cmsis-csolution/issues/295)

- Known issues:

  - Updating `launch.json` and `tasks.json` files does not preserve comments.

## 1.56.0

- New features:

  - The [**Software Components**](https://mdk-packs.github.io/vscode-cmsis-solution-docs/manage_components.html) view has been redesigned and uses the csolution tool
    from the CMSIS-Toolbox included in the extension for consistency with the command line.
  - The [**Manage Solution**](https://mdk-packs.github.io/vscode-cmsis-solution-docs/manage_settings.html) view adds the selection of a debug adapter supported by the
    [**Arm CMSIS Debugger**](https://marketplace.visualstudio.com/items?itemName=Arm.vscode-cmsis-debugger) extension.
    - The selection is stored in the active `*.csolution.yml` as default [`target-set`](https://open-cmsis-pack.github.io/cmsis-toolbox/YML-Input-Format/#target-set) for the active `target-type`.
    - If no `debugger:` is specified for the default `target-set` but the selected board specifies an [on-board debug adapter](https://open-cmsis-pack.github.io/Open-CMSIS-Pack-Spec/main/html/pdsc_boards_pg.html#element_board_debugProbe),
      this information is taken from `.cbuild-run.yml`. and a default `target-set` is used.
  - The **Views and More Actions...** menu available from the [**CMSIS-View**](https://mdk-packs.github.io/vscode-cmsis-solution-docs/debug.html#cmsis-view) has now a **Target information** entry.
    Click [**Target information**](https://mdk-packs.github.io/vscode-cmsis-solution-docs/create_app.html#check-target-information) to display information about the connected hardware.

- Solved issues:

  - Drop down box search filter handle matches on categories and items

- Info:

  - The location of `*.cbuild-run.yml` and `*.cbuild.yml` files is now consistently retrieved from the `*.cbuild-idx.yml` file for the commands `getCbuildRunFile` and `getBinaryFile(s)` which used hard-coded paths previously.

- Known issues:

  - Updating `launch.json` and `tasks.json` files does not preserve comments.

## 1.54.0

- New features:

  - New features require [CMSIS-Toolbox v2.9.0](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/releases/tag/2.9.0)
    or later. Update your workspace's `vcpkg-configuration.json` file accordingly.
  - The CMSIS Solution extension integrates with the [Arm CMSIS Debugger extension](https://marketplace.visualstudio.com/items?itemName=Arm.vscode-cmsis-debugger) adding action buttons and commands required for [debugging an application](https://mdk-packs.github.io/vscode-cmsis-solution-docs/debug.html#cmsis-view).
    - If a target-type specifies the node [`target-set:`](https://open-cmsis-pack.github.io/cmsis-toolbox/YML-Input-Format/#target-set) `cbuild` is launched for the active target-set instead of the context-set specified in `*.cbuild-set.yml`. In addition the selected contexts from **Manage Solution** dialog are stored in the `target-set` of the active `target-type`.
    - If a debug adapter is specified by the `*.cbuild-run.yml`, configurations are generated in `launch.json` and `tasks.json` based on the debug adapter templates specified in the [debug adapter registry](https://github.com/Open-CMSIS-Pack/debug-adapter-registry).
  - **Manage Solution** no longer supports the configuration of context specific "Run" and "Debug" actions. Corresponding options are deprecated in the user settings of the workspace.
  - [Device configuration files](https://open-cmsis-pack.github.io/cmsis-toolbox/build-overview/#device-configuration) (*.dbgconf) are moved and renamed. The files can be accessed from group "Device: ..." in **CMSIS-View**.

- Solved issues:

  - The YAML parser for the CMSIS solution input files ensures that all specified numeric, hexadecimal and boolean
    values retain their format in full, no quotes are added on write back.

- Known issues:

  - Updating `launch.json` and `tasks.json` files does not preserve comments.

## 1.52.0

- New features:

  - The quick picker from the "Select Active Solution from workspace" menu lists available solutions in alphabetical order.
  - The Installation of a pack can be initiated via a URI `vscode://arm.cmsis-csolution/installpack?pack=<pack>` launching VS Code, using the installed CMSIS Solution extension to run `cpackget add -a <pack>`.

  - **Solution outline** view improvements:
    - A **Manage software components** button is now available to open the **Software Components** view also from **Components** item.
    - **Copy header file** buttons are available for header files listed under **constructed-files** or **Components** adding `#include "<header file>"` to the clipboard.
    - **Set Clangd Context** buttons are available at the project level to activate clangd for a given project context.
    - Local files with extension ***.md** (Markdown format) are opened in the markdown preview mode.

- Solved issues:

  - Newly created solutions no longer fail due to missing configuration files from selected components because `update-rte` is now executed.
  - Fixed `command:cmsis-csolution.getCbuildRunFile` to return the filename following the convention `<solution>+<target>.cbuild-run.yml` introduced in CMSIS-Toolbox 2.8.0.
  - Arm Compiler 6 pre-defines are consistently exported into `.clangd` configuration files.
  - Reduce likelihood of duplicated calls to `cbuild setup` after converting µVision projects within the active workspace.
  - The YAML parser for the CMSIS solution input files ensures that all specified numbers retain their format. Double quotes are added on write back without causing any side effect.

- Known issues:

  - A `*.project.yml` that has components with for-context attributes might loose settings. ([ARM-software/vscode-cmsis-csolution#211](https://github.com/ARM-software/vscode-cmsis-csolution/issues/211)).
  - Missing source files in `*.cgen.yml` after generating code in CubeMX. ([ARM-software/vscode-cmsis-csolution#206](https://github.com/ARM-software/vscode-cmsis-csolution/issues/206), [Open-CMSIS-Pack/generator-bridge#129](https://github.com/Open-CMSIS-Pack/generator-bridge/issues/129)).

## 1.50.0

- New features:

  - The **Configuration Wizard** supports [Debug Configuration Files (*.dbgconf)](https://open-cmsis-pack.github.io/Open-CMSIS-Pack-Spec/main/html/pdsc_family_pg.html#element_debugvars) which, starting with **CMSIS-Toolbox 2.8.0**, are treated like [component configuration files](https://open-cmsis-pack.github.io/cmsis-toolbox/build-overview/#plm-of-configuration-files) from a Cclass="Device" component.
  - Pop-up notification added when launching a generator failed. The **CMSIS Solution** output channel displays by default.
  - Pop-up notification added if a csolution file is detected in the workspace when launching a µVision to CMSIS Solution conversion. You can choose to overwrite the existing csolution file.
  - The extension includes the CMSIS Solution schema files from the latest published CMSIS-Toolbox version (2.8.0).
  - The extension includes the latest published µVision to CMSIS Solution converter (1.6.0).

- Solved issues:

  - When adding a local PDSC file using `cpackget` the <timestamp> tag in local_repository.pidx must not be empty.
  - The deprecated [**CMSIS Solution Extension API version 1.0**](https://www.npmjs.com/package/@arm-software/vscode-cmsis-csolution) was removed. You must now use Version 2.0.
  - [A full list of resolved issues is available on GitHub](https://github.com/orgs/ARM-software/projects/10/views/10).

- Known issues:

  - When installing a local software pack with `cpackget` the [pack index is updated unnecessarily](https://github.com/Open-CMSIS-Pack/cpackget/issues/404).

## 1.48.0

- New features:

  - The **CMSIS View** shows the board and device for the active target.
  - The **CMSIS View** provides access to documentation for the board, device, and components.
  - The **Views and More Actions...** menu available from the **CMSIS View** has now a **Help** entry. Click **Help** to open the CMSIS Solution documentation.
  - The context help in the editor has been enhanced for *csolution project files*. Documentation links are provided when you move your mouse over the different elements.

- Solved issues:

  - The **Create Solution** view now presents the correct templates from packs.
  - [A full list of resolved issues is available on GitHub](https://github.com/orgs/ARM-software/projects/10/views/8).

- Known issues:

  - The layers and templates displayed in the **Create Solution** view are only taken from installed CMSIS software packs.
  - Software components from layers of inactive target types incorrectly display in the **Software Components** view in addition to the ones from the active target type.
  - When installing a local software pack with `cpackget`, (a) an [incorrect empty \<timestamp\> is created](https://github.com/Open-CMSIS-Pack/cpackget/issues/421), and (b) the [pack index is downloaded](https://github.com/Open-CMSIS-Pack/cpackget/issues/404).

## 1.46.0

- New features:

  - This version of the extension is targeted for use with [**CMSIS-Toolbox 2.7**](https://open-cmsis-pack.github.io/cmsis-toolbox/#revision-history).
  - The [**CMSIS Solution Extension API version 2.0**](https://www.npmjs.com/package/@arm-software/vscode-cmsis-csolution) is available on npm and gives access to all available boards and devices, their associated examples, and the ability to copy and build a selected example for use by other Visual Studio Code extensions.
  - Improvements to the CMSIS **Solution outline** view include: book icons to open documentation for API header files, count badges on components, **Add New Group** buttons at the project level, and improved default collapse settings.

- Solved issues:

  - CMSIS solution projects using a `yaml` file extension are loaded correctly again.
  - To access recently published pack versions, you must run `cpackget update-index --sparse`: Now the pack index is automatically updated by `cpackget` once a day.
  - If you are using CMSIS-Toolbox for the first time, you must manually initialize the CMSIS-Pack root directory with `cpackget init https://www.keil.com/pack/index.pidx`: Now the CMSIS-Pack root directory is initialized automatically if it does not exist yet.
  - After manually installing a CMSIS software pack, this version of the extension re-reads the package description files of the installed CMSIS software packs every time `cpackget` has added or removed a pack.

- Known issues:

  - The layers and templates displayed in the **Create Solution** view are only taken from installed CMSIS software packs.
  - Software components from layers of inactive target types incorrectly display in the **Software Components** view in addition to the ones from the active target type.
  - The pack installer updates the pack index even when installing a local CMSIS software pack file.

## 1.44.0

- New features:

  - The CMSIS status bar has been enhanced with a busy indicator and shows error and warning messages from CMSIS-Toolbox.
  - When the **Use Web Services** setting is enabled, the **Create new solution** view uses the internet database in addition to installed packs to display devices, boards, and examples.
  - For components, the **CMSIS** view now supports access to documentation from packs.

- Solved issues:

  - Software components from layers or generators display in the **Software Components** view.
  - In the **Manage Solution** view, the issues occurring when changing the context set configuration have now been solved.
  - [clangd](https://marketplace.visualstudio.com/items?itemName=llvm-vs-code-extensions.vscode-clangd) now supports code completion, compile errors, and go-to-definition for all active contexts.

- Known issues:

  - When using this extension for the first time in combination with the [Arm Environment Manager](https://marketplace.visualstudio.com/items?itemName=Arm.environment-manager), development tools are pre-installed. While this is happening, "Loading..." displays, which is misleading. You can check how the download process is progressing in **View** > **Output** > **Arm Tools** category.

## 1.40.0

- New features:

  - This version of the extension integrates [CMSIS-Toolbox 2.6](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/README.md#revision-history) with [CMake backend](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/build-operation.md).
  - The CMSIS Solution view has been improved based on [Build Information Files](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/YML-CBuild-Format.md).
    - Interfaces with [STM32CubeMX](https://www.st.com/en/development-tools/stm32cubemx.html) and [MCUXpresso Config Tools](https://www.nxp.com/design/design-center/software/development-software/mcuxpresso-software-and-tools-/mcuxpresso-config-tools-pins-clocks-and-peripherals:MCUXpresso-Config-Tools) added.
    - Easy access to [linker scripts](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/build-overview.md#linker-script-management), optional with Configuration Wizard annotations.
    - [Toolchain agnostic](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/build-overview.md#toolchain-agnostic-project) with support for Arm Compiler 6, GCC, IAR, and LLVM.
    - Supports for [software layers](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/build-overview.md#software-layers) and device-agnostic [reference applications](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/ReferenceApplications.md).
  - Dependency on [Arm Environment Manager](https://marketplace.visualstudio.com/items?itemName=Arm.environment-manager) removed, allowing flexible integration with other VS Code extensions.
  - [clangd](https://marketplace.visualstudio.com/items?itemName=llvm-vs-code-extensions.vscode-clangd) now supports code completion, compile errors, and go-to-definition across a whole project.
  - Option that enables the `--pack` option to download missing software packs using [cpackget](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/build-tools.md#cpackget-invocation) added.

- Known issues:

  - The [Arm Environment Manager](https://marketplace.visualstudio.com/items?itemName=Arm.environment-manager) takes a long time to load the first time you use it because all the default tool versions are downloaded and installed. You can check the installation progress in **View** > **Output** (Ctrl+Shift+U or Cmd+Shift+U). Select **Arm Tools** in the drop-down list.
  - The **Create new solution** view only accesses web-based examples from public packs or published repositories. Examples from local packs do not display yet.
  - You must manually download [Device Family Packs](https://www.keil.arm.com/devices/) and [Board Support Packs](https://www.keil.arm.com/boards/) using [cpackget](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/build-tools.md#cpackget-invocation) to start projects.
  - Software components from layers or generators do not display in the **Software Components** view.
  - To access recently published pack versions, you must run: `cpackget update-index --sparse`.
  - If you are using CMSIS-Toolbox for the first time, you must manually initialize the CMSIS-Pack root directory: `cpackget init https://www.keil.com/pack/index.pidx`.

## v1.38.0

- API extension:
  - query boards and devices
  - create csolution
- Sync with CMSIS-toolbox 2.5.0:
  - use 2.5.0 schemas
  - call `cbuild setup`
- Improvements to the μVision to csolution converter (uv2csolution 1.5.0):
  - Converted project files require CMSIS-Toolbox 2.4.0 or higher.
  - Fixed: conversion of μVision 5.40 projects using global generator CubeMX failing with "Errors: EOF".
  - Fixed: components with unchecked "Include in target build" listed under components node.
  - Fixes for new CMakeLists.txt generator `cbuild2cmake` in CMSIS-Toolbox 2.4.0 and higher:
    - Using "define-asm" node to set assembler specific defines.
    - Removal of duplicated modules contributed by both `*.gpdsc` and `*.uvprojx` file resulting in linker error about duplicated symbols.

## 1.37.0

- `Activate solution` prevented from opening CMSIS view.

## 1.36.0

- Show `open solution` command on the folders containing csolution files.
- Compilation command file loaded from inside the out folder instead of tmp folder.
- Allow to override uv2csolution path using environment variables.
- `Open solution` renamed to `Activate solution`.
- Create Solution Dialog: Replaced "Examples" dropdown with an TreeView including a search box.
- Fixed an issue where .clangd was not created.

## 1.35.0

- Improvements to the μVision to csolution converter:
  - Evaluation of new optimization value "-Omax".
  - Performing error handling before generating scatter file.
  - Fixing "Enable all warnings" for AC6 incorrectly specifies -Weverything.
  - Replacement of colon ':' characters in group names with undersore.
  - Adding support for new optimization level "debug".
  - Improvement of error and warning messages by removing XML tags and rephrasing them to make them more readable.
  - Adding 'instances' node in csolution to support multiple instances of a component.
- Improve intellisense within header files.

## 1.34.9

- Dependency updates.

## 1.34.8

- Minor improvements.

## 1.34.7

- Component manager: Display solution name in packs filter dropdown.

## 1.34.6

- Bugfix: changing the selected target in the context selection UI when there are no selected projects now updates the view correctly.

## 1.34.5

- Config Wizard: Option `<y>` added to change a symbol name.

## 1.34.4

## 1.34.3

## 1.34.2

- Prefer csolution example projects from packs over µVision project examples.
- Open the correct directory after converting a µVision example project.
- Rename Clean command to Clean Output Directories.
- Extension API: added new createSolutionFromUri api to create a new csolution project from a uri project and solution directory.
- Component manager: when there is an error state caused by missing packs, show a button that installs the missing packs.
- Status bar: shows the currently selected contexts.

## 1.34.1

- Fix duplication of quick fix code actions.

## 1.34.0

- Update YAML schemas to Toolbox 2.3.0.
- Fix template files copied from the pack cache readonly.
- Disable telemetry by default for SSK and HSK licenses.
- Sort boards in the create solution form.
- Show a help notification when the CMSIS Toolbox cannot be found.
- Fix vendor filtering of devices in the create solution form.

## 1.33.3

- Fix bug where `.clangd` files were not generating in some cases.

## 1.33.2

## 1.33.1

- Context selection: Refresh the view contents when source files are updated.
- Status bar: update icon to be the same as for context selection.
- Context selection: Display referenced projects, even if their source files are malformed.

## 1.33.0

- Context selection: add configuration UI for cprojects' run tasks and launch configurations.

## 1.32.2

- Create solution: There is now more of an indication that the board field is optional.
- Create solution: Automatically install packs when creating a new solution using the Create New Cmsis Solution.
- Component manager: Fix disappearing description when a component is selected.
- Added build, component class, components, files, layer, layers and software components icons to the solution outline view.

## 1.32.1

- Fix "clangd.applyFix already exists" errors when using the clangd extension.

## 1.32.0

- Improve clangd integration when using armclang. The compiler is queried for compiler specific defines to pass to the intellisense engine.
- Fix extension API build method so that it respects the given context argument.

## 1.31.0

- Add option to create files from [user code templates](https://open-cmsis-pack.github.io/Open-CMSIS-Pack-Spec/main/html/cp_PackTutorial.html#cp_CodeTemplates) provided by CMSIS software components. Click the plus icon next to a group in the solution view to get started.
- Active context: Editing "Run and Debug" options opens Arm Debugger editor for supported tasks and debug configurations.

## 1.30.0

- Add a new custom editor for configuration files based on [CMSIS Configuration Wizard Annotations](https://open-cmsis-pack.github.io/Open-CMSIS-Pack-Spec/main/html/configWizard.html). Open this with the "Open Preview" button at the top of the editor for a header file.
- Update the getHardwareAndToolchainInfo extension API to return additional information of board id, board pack id and device id.
- Do not set --schema flag when building solutions. This was causing problems due to this issue: <https://github.com/Open-CMSIS-Pack/devtools/issues/1345>.
- Fix updating the list of solutions in the workspace when the parent directory of a solution is deleted.

## 1.29.0

- Add editor links from solution files to referenced layer files, and from project files to layer files.
- Removed offerMicroVisionConversion setting. The extension no longer offers to convert µVision projects, so this setting is redundant.

## 1.28.0

- Update RTE files automatically when generating compile_commands.json. This fixes problems with intellisense when opening a csolution project for the first time.
- Remove deprecated cbuildPath and csolutionPath configuration properties. Use cmsisToolboxPath instead.
- Remove convertToCprj command. CPRJ files are still automatically generated when the csolution input files are changed. Also remove related autoGenerateCprj configuration property.
- Create Solutions: populate the solution name with a valid name when an example is chosen.

## 1.27.1

- Context selection: clicking run and debug edit links opens configuration files.

## 1.27.0

- Add new context selection UI, accessible from the cog icon in the solution view. This supports selecting a different build type for each project, and excluding projects from the build.
- Remove getBuildType, setBuildType, getTargetType, setTargetType, getProjectPath, setProject, and getCprjPath commands.
- Add getTargetPack command. This can be used in tasks.json and launch.json files to get the DFP CMSIS pack for the currently selected target.
- Automatically convert µVision examples downloaded with the new solution form to csolution.
- Component manager: helper text has been added to targets filter dropdown.
- Enable opening of the Software Components UI from the project level in the solution outline.
- Auto-select hardware in "create solution" UI if a development board is connected.

## 1.26.2

- Plus buttons next to groups in the outline view can be used to quickly add files to the group.
- Write converter output to a uv2csolution.log file when converting a µVision project to csolution.

## 1.26.1

- Create solution: if there is a workspace folder open, the solution location defaults to the parent directory of that folder.
- Add getBinaryFiles command.
- Shows a badge on the CMSIS icon before the view is opened for the first time.

## 1.26.0

- Automatically update PDSC manifests every week.
- Component manager: display pack install status.
- Component manager: Add project dropdown.
- Added icons to Create Solution and Software Components tabs.

## 1.25.0

- Fix parsing of component identifiers containing parentheses.
- Create solution form: fixed loading preview data when selecting the same hardware twice.
- Added run and debug configuration settings for solutions and projects.

## 1.24.4

- Fixed loading components from layer files.
- Show informative message in Software Components webview when there is no solution.

## 1.24.3

- Improvements to the μVision to csolution converter:
  - Consider CMSIS V6 by setting latest pack version prior to CMSIS v6 to fixed pack version "5.9.0" in CMSIS solution project.
  - Better handling of processor properties fpu, mve, trustzone, endianess and branch-protection.
  - Updating data in generated vcpkg-configuration.json file and avoid duplicating vcpkg entries.
  - Support multicore.
  - CMSIS csolution project is now generated if at least one target is faultless.
  - Improve warning and error messages.
  - Fixed: compile error when armmasm.exe is specified in uvprojx.
- Add target and build type labels to the solution outline view.
- Create solution: add option to clear the selected board.
- Show an option to convert a µVision project in the context menu in the solution outline rather than display a toast notification to do this.
- Use resolved packs defined in the cbuild-pack file if it is present.
- "Open CMSIS Solution" will now open the extension side panel.
- Install missing packs pop up: button to open file has been swapped to a button that opens the problems panel.

## 1.24.2

- Add explorer context menu item for opening a solution.
- Solution view: move create solution action to context menu and add open solution action.
- Create solution: change the heading for the compiler selection.
- Component manager: software components are filtered to solution by default.

## 1.24.1

- Create solution: improve generated .gitignore files.
- Create solution: generate default solution names.
- Create solution: add LLVM compiler to generated vcpkg file when it is selected.
- Create solution: constrain device hardware list by the mounted devices on the selected board.
- Only show output channels when they have content.

## 1.24.0

- Update YAML schemas to Toolbox 2.2.1.
- Fix line breaks in CMSIS Build Manager output channel.
- Create solution: can now select board-specific examples to use as a starting template for your application.
- Create solution: update the generated vcpkg-configuration.json to include the correct toolchain for the new solution.
- Disable icons for Build, Manage Software Components, Open Csolution File, Clean and Rebuild when there is no solution active.
- Updates the Manage Software Components icon.
- Component manager: add pack filtering capability.
- Create solution: add separate dropdown fields for boards and devices.

## 1.23.2

- Create solution: add target type field to set the name of the generated target type.

## 1.23.1

- Create solution: remove reference to device from generated project names.
- Create solution: remove checkbox controlling installation of missing packs. This is handled by default after creation.

## 1.23.0

- Create solution: remove feature flag.
- Add cmsis-csolution.getDeviceName command. This returns the CMSIS device name used by the current csolution context.
- The cdefault node present in the csolution file without a compiler sets the compiler to GCC.

## 1.22.0

- Create solution: only show toolchain options once a template is selected.
- Create solution: device name and vendor has moved from the generated cproject files to the target type.
- Create solution: show a loading spinner while loading hardware details.

## 1.21.0

- Create solution: sticky action buttons on small screens.

## 1.20.0

- Outline view: add action to clean the solution.
- The default build task now builds every project in the active solution.

## 1.19.0

- Improve reliability for intellisense support in header files.
- Add new options to the build task definition: `useContextSet`, `contexts`, `downloadPacks` and `schemaCheck`. `downloadPacks` defaults to true to automatically download missing packs during build.
- Add search filtering on device families and sub families when selecting a target in create solution.
- Write build command line to terminal when building a solution.
- Outline view: add build and rebuild options for the solution.
- Outline view: stop displaying projects, layers, groups and files that don't belong to selected context.
- Outline view: ensure project node only contains layers referenced by the project.
- Outline view: stop displaying component files that aren't relevant for selected device.

## 1.18.0

- Add search filter to work for vendors when selecting a target in create solution.
- Add create new solution to the new file menu option.

## 1.17.0

- Add welcome screen to solution outline view if there are no solutions in the workspace.
- Fixed project file paths for generated csolutions on windows.

## 1.16.0

- Reduce activity on VS Code startup to improve load performance.
- Remove duplicate and template files from the solution outline view.
- Remove component versions from cproject file.

## 1.15.0

- Improved styling of dropdowns in the create solution form.
- Remove the ability to change component versions from the components table.
- Create solution csolution and cproject files updated to use .yml file extension.

## 1.14.2

- Add cmsis-csolution.exclude setting for excluding files and folders in searches for csolution files.

## 1.14.1

- Show an error message in the create solution form when the processors cannot be determined for the target hardware.

## 1.14.0

- Simplify solution outline view: remove build types, target types, packs, and components not in the current context.

## 1.13.1

- Add Device Firmware Packs for all mounted devices on a board to newly created solutions.
- Add a main.c boiler plate file to newly created solutions.

## 1.13.0

- Improvements to the μVision to csolution converter:
  - Remove the linker option --list and --import-cmse-lib-out, replaced by $cmse-lib(<secure project>)$.
  - In the case user commands are specified in uvprojx converter displays warning to user to manually execute commands.
  - Consider the XML option `<CreateLib>` in uvprojx.
  - Add link to document for how to manually migrate AC5 to AC6 project.

## 1.12.3

- Added placeholder to hardware detail panel.

## 1.12.2

- Improve solution outline view performance.

## 1.12.1

- Move software components action to the Solution view.

## 1.12.0

- Fixed alignment the buttons at the bottom of the create solution webview.
- Add a new configuration setting to set the path of the CMSIS Toolbox. Deprecates the cmsis-csolution.cbuildPath and cmsis-csolution.csolutionPath settings.

## 1.11.8

- Fix components table reloading when a component is selected or deselected.

## 1.11.7

- Fix loading csolution files with cdefault enabled.
- Improved display of debug interfaces in the hardware detail panel.

## 1.11.5

- Simplify component validation fix sets, which have common mandatory dependencies and a single one-of dependency.

## 1.11.4

- Fix getProjectPath and getCprjPath commands.
- Add CMSIS:CORE component to generated solutions.
- Add LLVM compiler option to create solution form.

## 1.11.3

- Fix hardware resolution when using unpublished packs.

## 1.11.2

- Fix cmsis-csolution.getBinaryFile command.

## 1.11.1

- Prioritise device over board when resolving hardware for a context. This resolves some issues with managing software components in solutions targeting NXP hardware.
- Simplify the create solution form.

## 1.11.0

- Remove the Create Solutions Preview.

## 1.10.0

- Add compiler radio button selection options to the create solution panel.
- The solution view now correctly updates when the context is changed.
- Add a new `cmsis-csolution.getProcessorName` command. This returns the processor name for the current context, and can be used
to simplify tasks.json and launch.json files.
- Add directory selector to the Create Solution flow.
- Update document links to point to <https://pack-content.cmsis.io/>.

## 1.9.0

- Show API files in outline view.
- Identify config, template, and API files in the solution outline view.

## 1.8.0

- Clicking project and layer files in the solution view now expands the children instead of opening the file.
- Add a checkbox that installs required packs when a solution is created.
- Add getExamplesForBoard extension API for retrieving the list of examples from CMSIS Packs for specified device or board.

## 1.7.0

- Show component files in the solution outline view.

## 1.6.1

- Preserve scroll position and collapsed nodes when the Csolution view updates.

## 1.6.0

- Add support for converting µVision projects with C++ files.
- µVision converter now adds pack references in the cproject file, not the csolution file.
- Update Csolution schemas to 2.1.0.

## 1.5.3

- Add the error output to the popup that shows when a component fails to update.
- Fix display of "misc" in the Csolution view to show a single entry for each compiler, and a single 'All' entry when the compiler is not specified.

## 1.5.1

- Fix an issue where the CMSIS pack root preference is not respected.

## 1.5.0

- Check intellisense is enabled before registering the configuration.
- Add getHardwareAndToolchainInfo extension API for retrieving the selected device and toolchain for every context in a solution.
- Respect pack scope when resolving boards and devices.

## 1.4.3

- Software components table offers to clear the search filter when there are no results.

## 1.4.2

- Fix compilation for API types package.
- Add the "misc" option to "Layers in the solution view.
- Add the "misc" options to the solution in the outline view.

## 1.4.1

- Add the "misc" option to "Target types" in the solution view.
- Add the "misc" option to "Projects" in the solution view.

## 1.4.0

- Remove coreTools.path and coreTools.address settings.
- Refresh intellisense config on compile_commands.json changes.

## 1.3.3

- Fix the solution view for packs when the vendor is not specified.

## 1.3.2

- Fix parsing for misc settings with a "for-compiler" value.

## 1.3.1

- Clarify documentation for settings.
- Update Csolution YAML schemas to version 2.0.0.
- Fix "add pack" button in the Software Components Validation panel.

## 1.3.0

- Fix C/C++ intellisense integration on Windows.
- Only generate tasks.json and launch.json files if µVision conversion succeeds.
- Support cdefault files.

## 1.2.3

- Support clang compiler.

## 1.2.2

- Improve performance of component listing and validation in the Software Components UI.
- Software Components UI now resolves a board if it only has one revision.

## 1.2.0

- Support intellisense via Microsoft C/C++ extension.
- Add clean extension API.

## 1.1.0

- μVision converter now supports microlib.
- Activate the vcpkg environment after converting µVision to csolution.
- Add components from layers to the Software Components UI.

## 1.0.1

- Fix resolving components when the processor node is used in layer files.

## 1.0.0

- Update RTE directory by default when building csolutions.

## 0.31.0

- Fix support for devcontainers.
- Fix display of selected components in the Software Components UI when there is only one build context.
- Only show packs containing compatible components in the Software Components validation panel.
- Offer to convert μVision projects to csolution.

## 0.30.0

- Add toolchain, update-rte and jobs properties to the build task.
- Improve vcpkg-configuration.json generated from μVision conversion.
- Fixed "rebuild" option in extension build API.

## 0.29.0

- Rename convert command to "Convert μVision project to csolution".
- Improvements to the μVision to csolution converter:
  - Migrate to schema 2.0.
  - Do not generate backward slash in file paths. This fixes issues on non-Windows systems.
  - Generate vcpkg-configuration.json in project folder where csolution file is located.
  - Return an error in case the μVision project uses AC5.
- Add support for loading components from layer files.

## 0.28.0

- Build command now builds csolution files directly without needing cprj conversion step first.
- Compilation database for intellisense is now generated from csolution files rather than cprj.
- Add extension API for converting a μVision project to csolution.
- Update Csolution schema to 2.0.0-dev2.

## 0.27.0

- Improved μVision to csolution converter, including support for scatter file generation.
- Add support for converting uvmpw projects to csolution.

## 0.26.0

- Add context menu item to convert uvprojx files to csolution.
- Add support for adding packs to project files.

## 0.25.1

- Bugfix: fix build task hanging when the build process exits with an error.

## 0.25.0

- Add support for working with local packs using a local repository stored in $CMSIS_PACK_ROOT/.Local/local_repository.pidx.
- Add new items to the outline view. This is no longer behind the experimental features setting.
- Remove cmsis-csolution.remoteWorkspaceRoot configuration.

## 0.24.0

- Add support for multi-folder workspaces.
- Remove cmsis-csolution.outputPath configuration. Use the output controls in the csolution file instead.
- Remove cmsis-csolution.solutionPattern configuration. Only files ending in .csolution.yml or .csolution.yaml are considered to be solutions.

## 0.23.2

- Update the extension API to correctly handle paths case-insensitively on Windows.

## 0.23.1

- Fix passing `projectFilePath` to the `manageComponents` extension API.

## 0.23.0

- Add new csolution outline view to CMSIS panel that shows the structure, resources, and configuration of the solution. This is only shown when the "Experimental Features" setting is enabled.
- Extension API types are now available on NPM: [@arm-software/vscode-cmsis-csolution](https://www.npmjs.com/package/@arm-software/vscode-cmsis-csolution).

## 0.22.0

- Preserve comments and ordering when adding or removing components from cproject files.

## 0.21.0

- Show a notification when the active solution has missing packs.
- Add "Update PDSC manifests" command to load the latest CMSIS Pack data. Run this automatically on extension start.
- Fix highlighting missing packs when no version is specified.
- Fix loading packs from a pack cache initialised with cpackget.

## 0.20.0

- Add the origin CMSIS Pack to the component name tooltip in the Software Components view.
- Optimize for-contexts when writing components.

## 0.19.0

- Do not close Software Components UI when the csolution file is invalid.
- Add new default "All Targets" filter to the Software Components UI, showing components that are
compatible with all of the solution's target types.

## 0.18.0

- Only activate the extension if the workspace contains a csolution.
- Remove unpublished PDSC manifests that were previously shipped with the extension.

## 0.17.0

- Fixed spurious validation errors that appeared for some components in the Software Components view.

## 0.16.2

- Fix getBinaryFile command not honoring the output-dirs configuration in the *.csolution.yml file.

## 0.16.1

- Remove project name from getBinaryFile command output to match CMSIS Toolbox 1.5.0.

## 0.16.0

- Fix resolution of components without explicit versions.
- Update getBinaryFile command for CMSIS Toolbox 1.5.0.
- Show a component as selected even if it is not selected in all build types.

## 0.15.0

- Show documentation for component classes in the Software Components table.
- Fix clicking the status bar entry.
- Prevent content overflow of component name in the Software Components table.

## 0.14.0

- Allow component classes to be collapsed in the Software Components table.
- Fix updating context webview in the background.
- Validation fixes requiring adding components are now grouped together in the Software Components view.
- Validation panel dropdown UI updated to show fix counts.
- Expand or select rows on click in the Software Components table.
- Show component group documentation in the Software Components table.
- Added problem panel & csolution file diagnostics for "pack not installed" errors.
- Added quickfix for "pack not installed" errors.

## 0.13.0

- Add command to install a solution's missing packs `cmsis-csolution.installMissingPacks`.
- Improve performance of loading the list of devices for the Create Solution UI.
- Bugfix - applying fix sets to components that don't have variant, vendor, or version defined no longer fails.

## 0.12.0

- Add ability to select/deselect all components within a class or group in the software components view.
- Bugfix - correctly set build and target types to 'Undefined' when not set in solution file.
- Fix context view for solutions with no defined build or target types.

## 0.11.1

- Fix doc links in README.
- Fix docs publishing.

## 0.11.0

- Add resolution flow for components that have dependencies that are incompatible with the selected device/toolchain.
- Change name of undefined build or target types from Default to Undefined.
- Improve layout of Software Components view.
- Fix bug in component filtering where some components were being shown as available for incompatible devices.
- Fix bug in component resolution for partial references.
- Add component descriptions to components table.

## 0.10.0

- Improve performance of component validation.
- Handle partial component references in the manage components view.
- Add resolution flow for components that are not found in solution's packs - offer to add missing pack via validation panel.
- Filter validation errors of manage components by priority of importance.
- Prevent .clangd file from generating incorrectly at the root of the workspace.

## 0.9.0

- Clarify use of build type and target type in the create solutions UI.
- Manage components view no longer requires the experimental features flag.
- Fix converting MDK projects outside of the workspace (<https://github.com/ARM-software/vscode-cmsis-csolution/issues/4>).
- Add refresh command to reload the active solution.
- Reload the Manage Components view when the cproject file is changed.

## 0.8.1

- Remove apply and revert buttons from Manage Components. Changes are now saved to the csolution immediately.

## 0.8.0

- Add rebuild option to cbuild task. This cleans output directories before building.
- Add rebuild command.
- Fix selection for empty component vendor, variant, version and bundle in manage components.
- Update csolution YAML schemas to 1.3.0.

## 0.7.0

- Filter manage components view by target type.

## 0.6.1

- Clearly separate fix options for validation errors in the manage components view.
- Improve missing dependency reporting in manage components view.
- Fixed switching project for solutions with nested cproject files.

## 0.6.0

- Improved performance for loading device list in the new solution view.
- Highlight rows with validation errors in the experimental manage components view.
- Support switching bundle for unselected cclasses in the experimental manage components view.

## 0.5.5

- Fixed revert components in experimental manage components view.
- Fixed vendor, version and variant dropdowns in experimental manage components view.
- Run csolution conversion when the configured output directory or csolution path changes.
- Add component validation to experimental manage components view.

## 0.5.4

- Respect the CMSIS_PACK_ROOT environment variable.
- Updated context view icon.

## 0.5.3

- Fixed new solution creation flow on Windows.
- Fixed display of device vendors in the create solution UI.

## 0.5.1

- Fixed issue with CMSIS tools not starting.

## 0.5.0

- Remove build action bar, this is now provided by the Keil Studio extension pack.
- Added stying for the Create Solution form and Manage Components webviews.

## 0.2.0

### New Features

- Added 'Experimental Features' setting.

### Fixed

- Fixed context webview updates when the csolution file is modified.
- Handle solutions with no build or target types.
- Truncate project display names.
- Show relative paths to solution files in the contexts webview.
