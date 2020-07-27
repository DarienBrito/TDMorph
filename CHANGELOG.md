# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

# [Released]

## [2.0.0] (2nd quarter of 2020)

### New features
- Scripts are now possible in ElementsContainer and SceneLauncher
- New node: SceneLauncher, allows for fine detail control for preset launching and sequencing
- Possible to select change on start/end of morphing for parameters that are non-interpolatable
- Possible to use patterns via code (experimental)
- New patterns library created
- Integration with master clocks via the Beat and Ableton Link CHOPs, for LFO's and Patterns per slider
- Blending between two arbitrary parameters (experimental)
- Possible to drag and drop to re-order presets in the UI
- New node: PresetsAnimator, to convert stored presets to Animation COMP automatically
- New node: ExposeChannels, lets you grab all channels for each slider in a SlidersContainer
- Possibility to "Freeze" a given parameter, to avoid editing things by accident
- Two new interpolation modes (snapIn, snapOut)
- Jump to preset with Ctrl+left click (no interpolation)
- Morph to preset with Ctrl+right click (arbitrary "quick check" time, disregard of stored preset time)
- Cancel morphing wiht Ctrl+middle click
- Shift left-click over slider name to reset slider to original default value. 
- Now its possible to Stop/Play/Pause a current morphing in PresetManager
- Now possible to re-bind data using a bindings table
- New Universal "ElementsContainer" can host most parameter types
- All parameter types with corresponding UI's, except for File and Python supported.
- Blending of arbitary presets is now possible.

### Enhancements
- TDMorph is now faster when morphing, with architecture optimizations
- UI architecture and re-design, a great contribution by Roy Gerritsen from y=f(x) lab
- Hovering on preset now displays stored time and curve
- Optimized architecture, warrantied to not cook when idle
- New optional argument in SetPreset(morphTime=[some value]) allows to override stored preset time with arbitrary value
- Clean up and enhancemente of data flow for external signals in sliders
- Shift right-click over slider name to edit it (instead of double clicking)
- Sync is now a momentary button that writes the time value to all sliders, on any mode.
- Enhanced suite of tools to add ad-hoc modules
- TDMorph is now more efficient, with less unnecessary nodes
- Removed redundant comments and renamed functions to make code more readable

## Fixes
- Fixed problem on updating state of preset on opening/closing a project
- Deleted unnecessary code and improved comments for some methods

## [1.1.4] - 2020-7-04

### Added
- New node: PresetGrabber. Allows for accessing presets in tables that update on any preset change
  
### Fixes
- Fixed problem with clamping values in sliders

### Enhancements
- Presets are now an attribute in PresetManager and are dependable
- Presets can be accessed as PresetManager.Presets.getRaw()
- Deleted unnecessary code

## [1.1.3] - 2020-25-03
### Fixes
- Fixed an issue that caused strange parameters in slider on param drop
- Fixed an inconsistecy on index to set/store/delete presets. All begin now from 1
- Fixed an issue that prevented the use of toggles and menus with sliders
- Fixed an issue that altered presets when chaning morphing time while a recall was running

### Enhancements
- Changed logic of a couple elements for cleaner code
- Deleted unnecessary code

## [1.1.2] - 2020-09-03
### Fixes

- Renamed Parameters now persist across export/import 
- LFO mode now follows range on creation and persists when inspector is closed
- Launching presets and other python commands that got broken have been fixed
- Custom morph time issues after TD update are now fixed
- When reimporting from Json, parameters now preserver order
- Renaming TDmorph now causes no errors

## [1.1.0] - 2020-01-03
### Added

- Infrastructure for lfo and patterns support implemented (will not be yet fully released however)
- Fine control for mappings via a table
- Marker to show preset storage within the preset buttons
- Implemented a "pin" button, to collapse menu to just preset control for workflow enhancement
- Now its possible to change range of sliders to any arbitrary set of values
- Non interpolating parameters such as menus will change on start of trigger
- On completion signal for morphings can now be exported by the user
- Clocks for each slider can now be exported by the user
- Support for menu parameters, where range of slider is the number of items in menu
- Refactoring of SliderUI class to use properties (like it should)
- Deletion of unnecessary methods in SliderContainer and SliderUI classes
- Syncing affects also random distribution and interpolation curves

### Enhancements

- Sliders sub menu redesigned and optimized
- Robust system for auto-learn and mapping editing for OSC
- Less space taken by curve viewer
- Now possible to rename parameters by double-clicking on the name
- To save a preset shift-lclick, to delete it shift-rclick on the preset button
- Got rid of unnecesary  buttons for recall and save of presets
- Got rid of global shortcut for Lib. This allows for multiple instances of TDMorph in the same patch
- Binding is now from sliders to parameter instead of the other way around
- Attribute conversion for some methods, making the code more consistent
- Enhanced flow for changing parameters, more clear for developers

## [Released]

## [1.0.0] - 2019-31-12
- First official release
