# Preset Manager

**Part of the TDMorph Toolkit**  
Copyright © 2020–2025  
**Author:** [Darien Brito](https://www.darienbrito.com)  
**License:** [MIT License](https://opensource.org/license/mit)

---

## Overview

`extPresetManager` is the **core engine** of the TDMorph system for **TouchDesigner**.  
It manages the storage, retrieval, morphing, and randomization of parameter presets across multiple operators.

Unlike the UI components (`extUIExtension`, `extElementsContainer`, `extSceneLauncher`),  
this class operates entirely at the **data and logic level**, following a **Model–View–Controller (MVC)** structure — it acts as the **Model**, maintaining the preset data and communication with the `PresetMorpher` and `RandomGenerator`.

---

## Table of Contents

- [Architecture](#architecture)
- [Initialization](#initialization)
- [Stored Properties](#stored-properties)
- [Properties](#properties)
- [Private Methods](#private-methods)
- [Public Methods](#public-methods)
  - [Preset Management](#preset-management)
  - [Import and Export](#import-and-export)
  - [Morphing and Randomization](#morphing-and-randomization)
  - [State Retrieval](#state-retrieval)
  - [Path and Key Handling](#path-and-key-handling)
  - [Utility Methods](#utility-methods)
- [Design Philosophy](#design-philosophy)
- [Dependencies](#dependencies)

---

## Architecture

| **Attribute** | **Description** |
|----------------|-----------------|
| **Class** | `extPresetManager` |
| **Role** | Core preset logic for saving, recalling, morphing, and randomizing TouchDesigner parameters. |
| **Type** | Data Model |
| **Design Pattern** | Part of the TDMorph MVC system (acts as the Model). |
| **Usage Context** | Used for parameter management in presets, morphing systems, and automated transitions. |

---

## Initialization

```python
manager = op('PresetManager')
```
## Stored Properties

| **Property** | **Type** | **Description** |
|---------------|----------|-----------------|
| `Presets` | `dict` | Dictionary of stored presets. Each preset contains parameter states, morph time, curve, and random distribution. |
| `AutoMode` | `bool` | Enables automatic randomization or morphing when toggled. |
| `CurrentPresetName` | `str` | The currently active preset name. |
| `CurrentMorphCounter` | `int` | The current morph iteration count. |
| `LoopSequenceStatus` | `bool` | Whether preset sequence looping is active. |
| `RandomDistribution` | `str` | The random distribution method used for morphing. |
| `NumMorphs` | `int` | Number of morph steps per transition. |
| `MorphTime` | `float` | Duration (in seconds) of a morph transition. |
| `MorphCurve` | `str` | Type of interpolation curve used for morphing. |
| `ActivityStatus` | `bool` | Indicates if a morphing process is currently active. |
| `MorphingType` | `str` | Describes the current morphing method (linear, exponential, etc.). |
| `Blend` | `float` | Blend factor for interpolating between presets. |
| `BlendingActive` | `bool` | Whether preset blending mode is active. |
| `Lock` | `bool` | Prevents editing of presets when active. |

---

### Preset Management

- **`StorePreset(name=None)`**  
  Creates a new preset from the current state of all linked operators.  
  If no name is provided, uses the *Presetname* parameter.

- **`StorePresetWithData(name, data)`**  
  Stores a preset using provided data instead of reading live parameter states.

- **`DeletePreset(name=None)`**  
  Deletes a preset from storage.

- **`OverwriteCurrentPreset()`**  
  Overwrites the currently selected preset with new parameter values.

- **`OverwriteSinglePresetValue(name, item, val)`**  
  Overwrites a specific field in an existing preset.

- **`OverwritePresetsValue(item, val)`**  
  Overwrites a specific key/value pair across all presets.

- **`ClearPresets(overwriteWarning=False)`**  
  Clears all presets after confirmation.

- **`SetPreset(name=None)`**  
  Applies a preset immediately without morphing.  
  Automatically removes invalid nodes or parameters when encountered.

---

### Import and Export

- **`ExportJSON()`**  
  Exports all stored presets to a `.json` file for sharing or backup.

- **`ImportJSON()`**  
  Imports presets from a `.json` file.

- **`InjectPresets(presets)`**  
  Replaces all current presets with an externally provided dictionary.

---

### Morphing and Randomization

- **`MorphPreset(presetName, morphTime=None, morphCurve=None)`**  
  Morphs from the current state to the given preset using the specified curve and time.

- **`SetRandom(mode=None)`**  
  Randomizes parameter values, either automatically or on demand.

- **`MorphRandom(mode=None)`**  
  Morphs parameters toward randomized target values.

- **`StopMorphing()`**  
  Stops all ongoing morphing processes.

- **`PlayMorphing(play=True)`**  
  Starts or pauses morph playback.

- **`PresetsSequence(sortKeys=False, keysSequence=None)`**  
  Plays presets sequentially, in order or via custom key sequences.

- **`SetBlendingPresets(presetName, targetName)`**  
  Sets up two presets for blending.

- **`RandomizeGivenParameters(operatorIndex, names, mode=None)`**  
  Randomizes only the specified parameters on a given operator.

- **`MorphGivenParameters(operatorIndex, names, mode=None)`**  
  Morphs only the specified parameters on a given operator.

---

### State Retrieval

- **`GetStates(customWarning=None)`**  
  Returns a dictionary of all current parameter states for linked operators.

- **`GetEssentialStates()`**  
  Retrieves minimal morphing data for all linked operators.

- **`GetEssentialStatesFrom(presetName)`**  
  Retrieves morphing data from a specific preset.

---

### Path and Key Handling

- **`GetPresetsKeys()`**  
  Returns a list of all stored preset names.

- **`GetNumPresets()`**  
  Returns the total number of stored presets.

- **`GetMorphCurvesNames()`**  
  Returns available morph curve names from the `PresetMorpher`.

- **`GetRandomDistributionNames()`**  
  Returns all available random distribution modes from `RandomGenerator`.

- **`GetElementsPaths()`**  
  Retrieves paths to all linked operators.

- **`UpdatePath(oldPath, newPath)`**  
  Updates stored operator paths when components are renamed or moved.

---

### Utility Methods

- **`ReportResult(msg, title)`**  
  Displays a message box and prints debug output for user feedback.

---

## Design Philosophy

- **UI Independence:** Core logic is fully detached from any user interface.  
- **Data Transparency:** Presets stored as clean, JSON-serializable dictionaries.  
- **Extensibility:** Designed for subclassing and integration with various UI controllers.  
- **Robust Error Handling:** Validates operator paths and parameters dynamically.  
- **MVC Architecture:** Acts as the *Model* component, used by controllers like `extUIExtension` and `extSceneLauncher`.

---

## Dependencies

### TouchDesigner Components
- `PresetMorpher`  
- `Paths`  
- `RandomGenerator`  
- `TDResources`

### Python Libraries
- `TDStoreTools.StorageManager`  
- `re`  
- `json`  
- `itertools`  
- `sys`