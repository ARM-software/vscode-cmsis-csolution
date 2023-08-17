# Change Log

## 1.4.3

- Software components table offers to clear the search filter when there are no results.

## 1.4.2

- Fix compilation for API types package.
- Add the "misc" option to "Layers in the solution view
- Add the "misc" options to the solution in the outline view.

## 1.4.1

- Add the "misc" option to "Target types" in the solution view
- Add the "misc" option to "Projects" in the solution view

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
    - Migrate to schema 2.0
    - Do not generate backward slash in file paths. This fixes issues on non-Windows systems.
    - Generate vcpkg-configuration.json in project folder where csolution file is located
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
- Extension API types are now available on NPM: [@arm-software/vscode-cmsis-csolution](https://www.npmjs.com/package/@arm-software/vscode-cmsis-csolution)

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
- Fix converting MDK projects outside of the workspace (https://github.com/ARM-software/vscode-cmsis-csolution/issues/4).
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

- Added 'Experimental Features' setting

### Fixed

- Fixed context webview updates when the csolution file is modified.
- Handle solutions with no build or target types.
- Truncate project display names.
- Show relative paths to solution files in the contexts webview.
