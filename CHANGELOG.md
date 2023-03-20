# Change Log

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
