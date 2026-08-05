# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Since version 4, the free components carry their own version numbers rather than a single
toolkit version, because they now ship and update independently.

## [Open Toolkit 4.1.3] (3rd quarter of 2026)

PresetManager **4.1.3**, PresetInspector **1.5.4**, JSONTree **1.5.4**, ListView **1.0.3**.

The engine was substantially rewritten and the free tier grew from one component to four.
Presets written by older versions migrate automatically. Please report anything you find on the
[issue tracker](https://github.com/DarienBrito/TDMorph/issues).

### PresetManager

#### New features

- **Multi-track morphing engine.** Every tracked node can morph on its own clock, with its own duration, curve, shape coefficients, end mode, group and distribution. Enabled by the **Multi-Track Engine** toggle on the Options page, and **off by default**, so existing projects keep the 3.2 single-track behaviour unchanged.
- **Preset schema v2.** Timing moved from the top of a preset down into each tracked path, which is what makes per-track timing possible. Presets written by older versions migrate automatically and idempotently, with no data loss.
- **End modes per track:** hold, loop, ping-pong or advance.
- **Per-track auto sequences.** One node can walk its own preset or random cadence while its neighbours do something else.
- **Manual blending.** Load two presets and crossfade them by hand with a single factor, through the existing morph chain, with no clock running.
- **Curve-shape authoring.** Global `Curvea`, `Curveb` and `Curven` plus per-path columns in the paths editor. Coefficients reset to each curve's own defaults when the curve changes.
- **A View column in the paths editor** that opens or reuses one floating network pane on the tracked operator, selects it and frames it.
- **A test harness ships inside the component.** 171 checks. Pulse **Run Tests** on the `Tests` base.

#### Bug fixes

- **Stop now actually stops.** Stopping left the per-track auto cadences and both deferred queues armed, so a Stop issued while a track was completing was undone a frame later, restarting the clock.
- **Stopping no longer makes an untriggered track replay itself.** Track start times are absolute clock seconds, but stopping zeroed the clock, leaving stored starts in the future of the new epoch. A neighbouring track would freeze and later run a morph nobody asked for.
- **A deleted parameter no longer aborts the whole morph.** A stored parameter the user had since removed took down every other track with it. Missing names are now skipped, with one message per target naming them.
- **The blend menus cannot hijack a running morph.** Changing preset A or B while blending was off still overwrote the values of a morph in progress.
- **Loading a preset no longer rewrites your session defaults.** A loaded preset permanently replaced the session morph time, curve and distribution, so a later random morph ran at the preset's duration and ignored your global setting. Preset timing is now scoped to its own trigger. An explicit `morphTime` or `morphCurve` you pass in is still deliberate and still persists.
- **A morph time you pass in now wins over the times stored in the preset.** With multi-track on, an override was accepted and then ignored because each track fell back to its own stored duration.
- **A morph of zero seconds never finished.** It reached the target and left the engine running and cooking at rest, and the next morph started from stale state.
- **Importing a preset file written by an older version could not be morphed.** Import and inject now migrate the file instead of storing it as-is.
- **Migration no longer drops the curve shape.** A preset carried over from v1 lost its shape coefficients, so an Easein curve reached its target about a quarter of the way through.
- **Importing presets held by another component works.** The validation guarding against malformed payloads rejected TouchDesigner's own stored dictionaries.
- Re-storing a preset no longer flattens its per-track end mode, group and quantize settings.
- A preset sequence with an explicit key list no longer raises an index error.
- Malformed data passed to `InjectPresets` is now rejected on the way in, rather than surfacing much later as an unrelated error.
- Resetting the morph time no longer gives an instant morph. The value and the default were 2 and 0; both are 2.0 now.
- The shipped file no longer carries a leftover development path in its `Paths` storage.
- The morph count no longer ships at 2 with a default of 0.

#### Performance

- **Nothing cooks when idle.** The master clock is now a Timer CHOP that runs only while morphing, replacing an always-dirty Speed CHOP and a force-cook keep-alive. A stopped timer is clean, so the whole chain idles.
- **Cached parameter writeback** and **in-place channel updates**: about 4.6x faster on the hot path (351 µs to 75 µs for 400 channels).

#### Changed

- **The paths editor is now the owned MIT ListView**, replacing the Derivative Paths Lister. **PresetManager carries zero third-party content.** Every column it had is kept.
- Curves are consolidated into `curveLib` (16 functions plus their defaults). The legacy `CurvesGenerator` chain is gone.
- Several methods were removed or renamed. See the [API reference](Documentation/PresetManager.md#removed-since-32) for the full list and its replacements.

### PresetInspector (new to this repository)

The preset viewer and value editor, previously bundled, now ships here as its own MIT component at **1.5.4**. Attach it to a PresetManager to browse every stored preset as a tree, or point it at a JSON file. Values are editable, and write-back is guarded so a refused write is reported rather than silently dropped.

### JSONTree (new)

A reusable collapsible JSON tree viewer and inline editor at **1.5.4**, built on the native `listCOMP`. Search, expand and collapse, type-coloured values, editable leaves, and schema-aware rendering that collapses a TDMorph parameter dict into a single readable row. This is the viewer embedded in PresetInspector, released standalone so it can be used for any JSON inside TouchDesigner.

### ListView (new)

A reusable flat-columnar list widget at **1.0.3**, built on the native `listCOMP`. Declarative column spec, inline editing with type coercion, drag-to-resize columns, drag-to-reorder rows, and a pluggable Callbacks module. It is the widget the PresetManager paths editor and the SceneLauncher lists are built on, released standalone and MIT so it can be used in commercial and closed-source work.

# [Release]
## [3.2] (4th quarter of 2025)


### PresetManager

#### Bug fixes

- Improved help for filtering patterns (right-click the filter column to get suggestions).
- Expanded README help for regular expressions (right-click the filter column and select Help).
- Improved PresetManager callback system and fixed a bug that caused inconsistent triggering.

#### New features

- Added new Inspector utility node with text-based preset editing. Connect it to your PresetManager to fetch and manually overwrite presets as needed.
- Made MorphType property dependable.

### Parameter Morpher

#### Bug fixes

- Fixed dependable dictionary error occurring on save in recent TD versions.
- Streamlined code by removing unnecessary manual table editing options.
- Fixed MIDI and OSC mapping mechanisms.
- Resolved multiple issues introduced by recent TD updates.
- Simplified dropdown menus; codebase is now smaller and cleaner.
- Refactored several components for improved simplicity and compactness.
- Fixed an issue preventing toggles and menus from randomizing in certain cases.
- Fixed an issue where locks for non-interpolatable parameters were ignored when ivoking presets.

#### New features

- Improved Inspector functionality for MIDI and OSC mappings.
- Added Perform Mode to reduce memory usage after preset setup.
- TDMorph now supports all parameter types except Header, Sequence, and Python.
- Scripts can still be launched per preset via Add Script in an ElementsContainer.
- Added randomization and locking for non-interpolatable elements.
- Global and Local modes are now stored independently, enabling separate timelines, cuves, and distributions per preset.
- Int sliders do not try to interpolate anymore, therefore behaving more consistently.

### Scene Launcher

#### Bug fixes

- Fixed numerous issues caused by latest TD updates
- Fixed an issue that prevented scripts from being triggered on "Sequence" action.
- Fiex an issue that computed delay times erronously on "Sequence" action.

#### New features

- Removed transport functionality, as it does not align with the tool's purpose.

# [Alpha release]
## [3.1.1] (3st quarter of 2024)

#### Bug fixes

- Fixed font issue discrepancy on Mac that showed empty text on components. Default is now Verdana and Material Design Icons, which work on both systems.

# [Alpha release]
## [3.1.0] (2st quarter of 2024)

This release was mainly focused in solving things that got broken along the way with TD updates. It has a better implementation of nodes, a cleaner and update UI and an overall smaller memory footprint. So should be lighter and faster.

### PresetManager

#### New features

- Added pulse to "overwrite" current target preset, which speeds up workflow. Before one had to change the name of preset and store. Now this is done in a single click under the "Actions" header.

- Added callback functions to trigger events on completion:
	onMorphingStart()
	onMorphingEnd()
	onPresetCall()

#### Bug fixes

- Timing possibilites were broken in latest TD versions, due to a change in timer's "Active" parameter from a toggle to a menu
- Various issues apperared on cloning with latest version, not sure why precisely... but these have been fixed.
- Fixed a bunch of broken functionality in quantization

### Parameter Morpher

#### Bug fixes

- All PresetManager-related issues

#### Changes

- Re-designed the way UI elements are created
- All code is now moved to a "Modules" base and all classes now reference the code with selects. This reduces file size and is dramatically easier to mantain.
- Updated certain UI elements to use current standards, such as replacement of dropdown menu's and text operators with latest optimized versions.
- Removed a lot of unnecessary parameters and code on low level, which made things lighter and easier to understand for developers.

### Scene Launcher

#### New features

- Added callback functions to trigger events on completion:
	onMorphingStart()
	onMorphingEnd()
	onPresetCall()

#### Changes

- Similar UI and code enhancements as with "Parameter Morpher"

# [Beta release]
## [3.0.0] (1st quarter of 2023)

### PresetManager

#### New features

- New node addition mechanism via UI drag and drop
- Paths can now be updated automatically 
- Paths can be edited manually too, although the automatic method is recommended
- Each node can now have its own wildcard to capture specific parameters
- Capturing wildcard support has been extended to regular expressions
- Added interpolation output to PresetMorpher
- Added blending possibilities on the COMP level

#### Bug fixes

- An inconsistency that prevented adding new parameters after creating some presets
- An error caused by the new Header parameter type
- An inefficiency that made settings jump when interpolating large data-sets
- A redundancy that unnecessarily extra data for each parameter
- An excess of dependable storage has been removed 
- Completion signal for morphings is now reliable.

#### Changes

- Replaced all calls of getattr and setattr, which are slow, with direct dictionary calls
- The input table to specify paths has been removed
- PresetManager now relies on the internal Path component for node paths
- Interpolation curves have been changed to CPU-based, to ensure frame-by-frame synchronicity
- RandomMorph method was renamed to MorphRandom
- Randomize method renamed to SetRandom
- SetPreset method renamed to MorphPreset
- JumpToPreset method renamed to SetPreset
- Saw, Step, Perlin and Simplex interpolations have been removed
- Removed paths specification via a table, which should be done now via de given UI
- Renamed and re-structured various parameters in the Base
- Two new parameters as A and B targets for blending have been added at the Base level
- All extUI extension classes have been removed (better design)

### ParameterMorpher 

#### New features

- Added "Freeze" mode, which disables all interaction for sliders and randomizations to avoid unwanted changes when a set of desired parameters is found.

#### Bug fixes

- Many inefficiencies have been resolved and the UI should feel lighter.
- File size is greatly reduced.
- A lot of other things I did not keep track of :P 

#### Changes

- Replaced all calls of getattr and setattr, which are slow, with direct dictionary calls
- Previously this was the whole library, which now has been rebuilt to be a UI front-end only
- Because of that change this is now called the Parameter Morpher
- Internal path allocation has been completely revamped
- All extUI extension classes have been removed (better design)

#### Workflows

- If you delete all elements in a container and there were presets saved,
if you recreate the elements and use global mode the presets will still 
be there and functional for available elements. To make them work locally
as well resave the presets in global mode one by one and voila.

### Scene Launcher

#### Changes	

- Callbacks system has been refactored to a simpler model
- System-wide refactor of UIs. Should be faster and smoother.


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
