# extSceneLauncher.py

**Part of the TDMorph Toolkit**  
Copyright © 2020–2025  
**Author:** [Darien Brito](https://www.darienbrito.com)  
**License:** [MIT License](https://opensource.org/license/mit)

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

---

## Table of Contents

- [Initialization](#initialization)
- [Architecture](#architecture)
- [Stored Properties](#stored-properties)
- [Private Methods](#private-methods)
- [Properties](#properties)
- [Public Methods](#public-methods)
  - [Scene Management](#scene-management)
  - [Preset and Morph Handling](#preset-and-morph-handling)
  - [Actions and Transport Control](#actions-and-transport-control)
  - [Import and Export](#import-and-export)
  - [Utility and UI Methods](#utility-and-ui-methods)
  - [Animation](#animation)
- [Design Philosophy](#design-philosophy)
- [Dependencies](#dependencies)
- [See Also](#see-also)

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

- **`WritePresets()`**  
  Writes the current list of presets into the internal presets table.

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

---

### Preset and Morph Handling

- **`GetCurrentCellValue(cellName)`**  
  Retrieves a cell’s value from the current scene row.

- **`SetCellColor(row, col, color)`**  
  Overlays a color highlight for a given scene cell in the list.

- **`GetMorphCurves()`**  
  Returns a list of available morph curves from the attached `PresetManager`.

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

- **`LaunchScene(target)`**  
  Launches a scene by its table index number.

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
- `PresetManager`  
- `listPresets/lister`  
- `listScenes/lister`  
- `Utils/ColorPicker2`  
- `Actions/chopexec1`  
- `TDResources` *(for popups and dialogs)*

### Python Libraries
- `TDStoreTools.StorageManager`  
- `json`  
- `random`  
- `copy`
