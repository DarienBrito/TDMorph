# Scene Launcher

**Part of the TDMorph Toolkit**  
Copyright © 2020–2026  
**Author:** [Darien Brito](https://www.darienbrito.com)  
**License:** **PROPRIETARY. Licensed, not sold.**  
**Version:** 4.3.6

> SceneLauncher is a **commercial** component of the TDMorph toolkit, governed by the
> SceneLauncher EULA (see the `LICENSE` operator inside the component). No redistribution,
> resale, sublicensing or sharing. No warranty.
>
> It is **not** MIT licensed and is not distributed from this repository. It is available
> through [Patreon](https://www.patreon.com/c/darienbrito). This page is reference
> documentation only.

---

## 4.3.4

- **Mapping MIDI or OSC to the morph curve or random distribution selector now works.**
  Learning a knob onto either looked like it worked and then had no effect: the selector
  moved internally while the visible dropdown and the value it sets stayed put. Every other
  mapped control was unaffected. ParameterMorpher 4.8.1 fixes the same fault; the two
  components carried identical code.

## 4.3.3

- **Test coverage only. Nothing in the component behaves differently** and your scenes and
  mappings are unaffected. The bundled test suite now presses each control in the menu and
  checks what actually happened (the row the transport moved to, the curve the selector
  seated, the map mode the icon entered), rather than only checking that the method behind
  it exists. The suite grows from 216 checks to 238.

---

## 4.3.2

- **Mapping a menu parameter now reaches its last item.** A learned menu mapping spans the
  full 0 to N range. Previously it stopped at N-1, and because TouchDesigner floors a menu
  value to an index, the last item was reachable from only 1 of 128 raw MIDI values while
  every other item got 8 or 9.
- **The header map icon is a crosshairs**, replacing the MIDI DIN plug it had inherited. One
  icon covers both protocols, so a MIDI connector was the wrong picture.

---

## 4.3.0: the MIDI/OSC mapping rebuild (breaking)

Version 4.3.0 replaces the MIDI/OSC mapping subsystem outright. **Mappings made in earlier versions are not carried forward**, and a few parameters changed name, so any mappings you already have need to be made again.

What changes for you:

- **One map mode, not two.** The separate MIDI and OSC icons in the header are now a single **Map** icon, shown whenever either a MIDI or an OSC input is wired on the Config page. Click it, click any control, then move a fader, knob or key to bind it. Both protocols share one list.
- **One mapping list.** The `Mappings` parameter page is now **Manage Mappings** and **Clear All Mappings** (previously four pulses split across MIDI and OSC sections). The editor shows every mapping in one table.
- **Per-mapping range.** Each mapping carries its own **Min** and **Max**, editable in the list. Previously all MIDI mappings shared one global input range.
- **Soft takeover.** Each mapping can be set to `pickup`, which waits until the incoming control reaches the parameter's current value before taking over, instead of jumping to wherever the fader happens to sit. `jump` is the default and matches the old behaviour.
- **Dead mappings are visible.** If a mapped control is renamed or removed, the row is marked `(missing)` in the list rather than silently doing nothing, and can be cleared with **Prune dead mappings**.
- **Retired parameters:** `Clearmidimappings`, `Managemidimappings`, `Clearoscmappings`, `Manageoscmappings`, `Togglelocationmidi`, `Togglelocationosc`.

Anything can now be a mapping target, not just the built-in controls: a mapping stores a control and a parameter name, so any custom parameter can be driven.

---

## Overview

`extSceneLauncher` is a **scene-based preset launcher** in the TDMorph system for **TouchDesigner**.  
It provides a flexible and performance-oriented interface for triggering **“scenes”** — each representing a preset with its own duration, delay, morph curve, script, and follow action.

This class acts as an **alternative UI** for the PresetManager, allowing users to:
- Build and manage scenes visually.
- Link each scene to a preset target.
- Define morph timing and interpolation curves.
- Create follow actions (like *Next*, *Repeat*, *Random*, etc.).
- Export and import full scenes and presets as `.json` files.
- Automatically build animations from existing scenes.

### What changed in 4.x

- **It attaches an external PresetManager** through the `Presetmanager` parameter, and so
  inherits the shared multi-track engine: per-track timing, end modes, curve shapes and
  preset schema v2. See [PresetManager](PresetManager.md).
- **The scene and preset lists are owned `ListView` instances**, replacing the palette
  Listers. The MIDI and OSC mapping inspectors are an owned `listCOMP` editor. SceneLauncher
  carries no third-party content.
- **The ControlsMenu is fully themeable** from an 18-parameter `ControlsMenu` page on
  `Lib/Look`, with the root Colors page driving the accent and row colours.
- The OSC and MIDI header buttons appear only when the matching `Osc` and `Midi` CHOP
  parameters resolve, so the component ships showing four header icons rather than six.
- Ships **empty**: no scenes, no presets, `Presetmanager` blank. Attaching a PresetManager is
  the first step under [Getting started](#getting-started) below.

---

## Installation

1. Download `SceneLauncher.tox` from [Patreon](https://www.patreon.com/c/darienbrito).
2. Drag the `.tox` into your TouchDesigner network, or use **File > Import > Component**.
3. Click the component's viewer to open the panel.

**SceneLauncher needs a PresetManager.** It is a user interface for an engine it deliberately
does not contain, so on its own it has nothing to launch. PresetManager is free and MIT
licensed, from [this repository](../PresetManager/). Any component that already embeds one
works too, including a ParameterMorpher container's internal manager.

The licence terms are in the `LICENSE` operator inside the component.

## Getting started

The component opens **empty**: no scenes, and the `Presetmanager` parameter blank.

### 1. Give it a PresetManager with presets in it

Drop a PresetManager into your network, point it at the parameters you want, and store at
least two presets. A SceneLauncher attached to a manager with no presets will show an empty
target list and there will be nothing to cue.

### 2. Attach it

Set **`Presetmanager`** on the **Config** page to that component. The preset list on the right
of the panel fills in immediately.

If you attach a manager and the lists look stale, pulse **`Refresh`** on the same page.

### 3. Create a scene

<kbd>Right Click</kbd> empty space in the scene list and choose **New scene**.

The same menu holds the rest of the scene-level actions: *Duplicate*, *Clear scenes*,
*Clear actions*, *Clear scripts*, *Export presets*, *Import presets* and *Refresh*.

### 4. Point the scene at a preset

<kbd>Right Click</kbd> the scene's **Target** cell. A menu opens listing the preset names in
the attached manager. Pick one.

**Curve** and **Action** open on <kbd>Right Click</kbd> the same way: Curve chooses the
interpolation shape, Action chooses the follow action (*Next*, *Repeat*, *Random* and so on)
that fires when the scene finishes.

**Scene**, **Length**, **Delay** and **Script** are inline text cells instead: click and type.
The **color** swatch and the trash icon are left-click buttons.

A row reads, left to right: `#`, colour swatch, Scene, launch icon, Length, Delay, Target,
Curve, Action, Script, delete icon. Delay and Script are hidden unless `Enabledelays` and
`Enablescripting` are on, both of which ship enabled.

Note that editing a scene's **Length** or **Curve** also overwrites that value in the target
preset's own stored data. This is destructive and deliberate, matching the behaviour of
earlier versions: the scene is the authority on its own timing.

### 5. Launch it

Click the **launch icon** in the scene's row, the fourth column, just right of the scene name.

That icon is the only thing that launches a scene. Double-clicking any other cell is
deliberately inert, so editing a Curve or Action can never fire the scene by accident.

Build up a few scenes, give them follow actions, and the launcher will run them as a cue
list. `Totaldurationf` and `Totaldurations` on the **Info** page report the total.

### 6. Where to go next

The `Osc` and `Midi` parameters on the **Config** page take CHOP references. Wire either one
and the matching header icon appears, six icons instead of the four it ships with, giving you
auto-learn mapping for the transport controls.

Full key and mouse reference: [SHORTCUTS.md](../SHORTCUTS.md). Everything below this point is
the Python API.

---

## Table of Contents

- [Initialization](#initialization)
- [Architecture](#architecture)
- [Stored Properties](#stored-properties)
- [Public Methods](#public-methods)
  - [Scene Management](#scene-management)
  - [Preset and Morph Handling](#preset-and-morph-handling)
  - [Actions and Transport Control](#actions-and-transport-control)
  - [Import and Export](#import-and-export)
  - [Utility and UI Methods](#utility-and-ui-methods)
  - [Animation](#animation)
- [Design Philosophy](#design-philosophy)
- [Dependencies](#dependencies)

---

## Initialization

```python
launcher = op('SceneLauncher')
```

## Architecture

| **Attribute**      | **Description** |
|--------------------|-----------------|
| **Class**          | `extSceneLauncher` |
| **Role**           | Scene-based interface for controlling and launching presets. |
| **Type**           | UI Controller |
| **Design Pattern** | Part of the TDMorph MVC system. |
| **Usage Context**  | Used to trigger and manage timed preset transitions (“scenes”). |

## Stored Properties

| **Property** | **Type** | **Description** |
|---------------|----------|-----------------|
| `Scenes`      | `dict`   | Stores all created scenes and their metadata (name, duration, delay, target, curve, action, script). |
| `Sequential`  | `bool`   | Indicates whether the launcher is in sequential playback mode. |
| `Source` | `obj` | Reference to the associated `PresetManager`. |
| `Row` | `int` | The current selected row index. |
| `Col` | `int` | The current selected column index. |
| `Scene` | `int` | The currently active scene name. |
| `Target` | `str` | The preset target associated with the active scene. |

## Public Methods

### Scene Management

- **`LaunchScene(target)`**  
  Launches a scene by its table index number.

- **`CreateScene(name, target='None')`**  
  Creates a new scene entry with default parameters (length, delay, curve, color, etc.).

- **`DuplicateScene(name, sourceName)`**  
  Duplicates an existing scene, appending `_copy` or renaming to avoid overwriting.

- **`WriteScenes()`**  
  Writes all scene data to the UI table and updates total duration information.

- **`ClearActions()`**  
  Resets all scene “Action” values to `'None'`.

- **`ClearScripts()`**  
  Removes all script references from the scene table.

- **`EnableScripting(enable=True)`**  
  Enables or hides the *Script* column in the scene list.

- **`EnableDelays(enable=True)`**  
  Enables or hides the *Delay* column in the scene list.

- **`WritePresets()`**  
  Writes the current list of presets into the internal presets table.

---

### Preset and Morph Handling

- **`GetCurrentCellValue(cellName)`**  
  Retrieves a cell’s value from the current scene row.

- **`SetCellColor(row, col, color)`**  
  Overlays a color highlight for a given scene cell in the list.

- **`GetMorphCurves()`**  
  Returns a list of available morph curves from the attached `PresetManager`.

- **`SyncMorphCurveMenu()`**  
  Rebuilds the ControlsMenu CURVE selector from the attached `PresetManager`'s curve
  registry, so the two can never drift apart. Does nothing when no `PresetManager` is
  attached, leaving the existing menu in place.

- **`SetMorphCurve(index)`**  
  Applies a curve selection to the attached `PresetManager`. No-op when none is attached.

- **`SetRandomDistribution(index)`**  
  Applies a random-distribution selection to the attached `PresetManager`. No-op when none
  is attached.

- **`GetCueActions()`**  
  Returns a list of available follow actions (`None`, `Next`, `Repeat`, etc.).

- **`EnableFollowActions(enable=True)`**  
  Toggles the follow action system that triggers automatic scene transitions.

- **`DelayedPresetTrigger(target, length, curve)`**  
  Executes a delayed preset morph, using the scene’s timing and curve.

---

### Actions and Transport Control

Transport controls are linked to scene actions and follow modes.  
They allow stepping through, randomizing, or looping scenes.

- **`SequentialLaunch(data)`**  
  Handles the timing and triggering of sequential scene transitions.

- **`PerformAction(action, value=None)`**  
  Triggers an action from the transport menu (e.g., *Next*, *Stop*, *Repeat*).

---

### Import and Export

- **`ImportPresetsJSON()`**  
  Imports both presets and scenes from a `.json` file.  
  Also injects the preset data into the linked `PresetManager`.

- **`ExportPresetsJSON()`**  
  Exports all current scenes and presets into a single `.json` file.  
  Includes morph curve, timing, and follow action data.

---

### Utility and UI Methods

- **`ReportResult(msg, title)`**  
  Displays a popup dialog and prints debug information to the console.

- **`StandardPopMenu(info, items, callback)`**  
  Opens a contextual popup menu.

- **`StandardPopDialog(text, title, buttons, callback, details=None, textEntry=False)`**  
  Opens a custom dialog window.

---

### Animation

- **`CreateAnimation()`**  
  Builds a `PresetAnimator` using all existing scenes and presets.  
  Synthesizes presets with the scenes’ timing, delay, and curve data for animation playback.

---

## Design Philosophy

- **Scene-Oriented Workflow:** Treats presets as “cues” or “scenes” with their own transitions.  
- **Non-Destructive Editing:** Scenes can be created, duplicated, and reordered freely.  
- **Integration-Ready:** Connects seamlessly with `PresetManager` and `ParameterMorpher`.  
- **Automation-Driven:** Designed for theatre, installation, and live performance contexts where sequence automation is essential.  
- **UI-Independent Core:** Logic operates independently of specific interface designs.

---

## Dependencies

### TouchDesigner Components
- `PresetManager` *(external, attached through the `Presetmanager` parameter)*  
- `listScenes` and `listPresets` *(owned `ListView` instances, with `listScenesCallbacks` and `listPresetsCallbacks` supplying their behaviour)*  
- `Utils/ColorPicker2`  
- `Actions/chopexec1`  
- `Lib/Look` *(the ControlsMenu theme)*  
- `op.TDResources` *(TouchDesigner's own pop-up menu and dialog host)*

### Python Libraries
- `TDStoreTools.StorageManager`  
- `json`  
- `random`  
- `copy`
