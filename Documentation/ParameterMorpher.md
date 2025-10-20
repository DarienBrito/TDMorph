# ParameterMorpher

**Part of the TDMorph Toolkit**  
Copyright © 2020–2025  
**Author:** [Darien Brito](https://www.darienbrito.com)  
**License:** [MIT License](https://opensource.org/license/mit)

---

## Overview

The ParameterMorpher is comprised of various components. To access full functionality, you need to interact with bot the `extParameterMorpher` class and the `extElementsContainer` class.

## exParameterMorpher

The `extParameterMorpher` class is part of the **TDMorph** system for **TouchDesigner**.  
It manages **container creation**, **library tool instantiation**, and **parameter exposure** within the TDMorph module.  

This class serves as a **high-level manager** for creating interface elements, preset-related tools, and morphing utilities from the internal library.  
It adheres to a **Model–View–Controller (MVC)** structure, functioning as the *Model*—that is, the logic and data layer independent of UI interactions.

---

## Table of Contents

- [Architecture](#architecture)
- [Initialization](#initialization)
- [Private Methods](#private-methods)
- [Public Methods](#public-methods)
  - [Reporting and Retrieval](#reporting-and-retrieval)
  - [Container Management](#container-management)
  - [Preset Manager Integration](#preset-manager-integration)
  - [Library Object Creation](#library-object-creation)
  - [UI Layout Control](#ui-layout-control)
- [Design Philosophy](#design-philosophy)
- [Dependencies](#dependencies)

---

## Architecture

| **Attribute** | **Description** |
|----------------|-----------------|
| **Class** | `extParameterMorpher` |
| **Role** | Manages creation of containers, preset-related tools, and exposure of morphing data. |
| **Type** | Model / Logic Controller |
| **Design Pattern** | Part of the TDMorph MVC architecture. |
| **Usage Context** | Used internally to instantiate morphing-related utilities and connect Preset Managers to UI containers. |

---

## Initialization

```python
morpher = op('ParameterMorpher')
```
## Public Methods

### Container Management

- **`GetContainer(n)`**  
  Retrieves a specific container UI by index.  

- **`CreateContainer()`**  
  Creates a new container for slider-based UI elements and links it to the `Elements` component.  

---

### Preset Manager Integration

- **`ExposeTimers(x=0, y=0)`**  
  Creates a composite component exposing **Preset Manager timer channels**.  


- **`ExposeChannels(x=0, y=0)`**  
  Creates a component exposing all **parameter channels** of the UI sliders.  

---

### UI Layout Control

- **`ChangeOrientation(horizontal=False)`**  
  Changes the alignment of UI containers between horizontal and vertical layouts.  

### Reporting

- **`ReportResult(msg, title)`**  
  Displays a popup dialog in TouchDesigner and logs a formatted message to the console.  

---

## Design Philosophy

- **UI Independence:** Logic operates independently of any UI behavior.  
- **Modularity:** Provides an interface layer for morphing and preset operations without visual dependencies.  
- **Automation-Friendly:** Allows automatic generation of morphing tools and managers in project setups.  
- **Extensibility:** Encourages addition of new library components without structural changes.  
- **MVC Integrity:** Respects the TDMorph Model–View–Controller separation of concerns.

---

## extElementsContainer

---

## Overview

The `extElementsContainer` class manages **groups of UI elements** (sliders, toggles, menus, etc.) in **TDMorph**, providing a high-level interface between the user interface and the internal `PresetManager`.  

It acts as a **UI-focused controller**, handling element creation, parameter binding, preset management, and synchronization between visual and logical layers.  

This class is primarily used to create and manage **parameter-linked sliders** for morphing and randomization within **TouchDesigner**.

---

## Table of Contents

- [Architecture](#architecture)
- [Stored Properties](#stored-properties)
- [Private Methods](#private-methods)
- [Public Methods](#public-methods)
  - [Container and UI Management](#container-and-ui-management)
  - [Preset Management](#preset-management)
  - [Import and Export](#import-and-export)
  - [Randomization and Morphing](#randomization-and-morphing)
  - [Sequence Control](#sequence-control)
  - [Utility and Miscellaneous](#utility-and-miscellaneous)
- [Callbacks](#callbacks)
- [Design Philosophy](#design-philosophy)
- [Dependencies](#dependencies)

---

## Architecture

| **Attribute** | **Description** |
|----------------|-----------------|
| **Class** | `extElementsContainer` |
| **Role** | Manages groups of morphing UI elements for parameter control. |
| **Type** | UI Controller / Manager |
| **Design Pattern** | Part of the TDMorph MVC architecture. |
| **Usage Context** | Used to create UI bindings, manage presets, randomization, and morph transitions. |

---

## Stored Properties

| **Property** | **Type** | **Description** |
|---------------|----------|-----------------|
| `BindedPaths` | `dict` | Dictionary mapping cross-check names to binding data for parameters. |
| `containerName` | `str` | Name of the container instance. |
| `NumberOfElements` | `int` | Number of elements contained in the UI container. |
| `GlobalStatus` | `bool` | Whether global morphing and randomization are enabled. |

---

### Container and UI Management

- **`Name`** *(property)*  
  Gets or sets the container’s name.  

- **`Delete()`**  
  Deletes all UI elements and destroys the container panel.  

- **`UpdateSize(sizeLimit=720)`**  
  Adjusts the height of the container based on its content.  

- **`HardSyncLFOs()`**  
  Resynchronizes all internal LFOs across contained elements.  

- **`ChangePresetsNum(newVal)`**  
  Changes the number of presets available in the container.  

- **`GetBindedKeys()`**  
  Returns a list of all keys from the `BindedPaths` dictionary.  

- **`GetPresetManager()`**  
  Returns the internal `PresetManager` component reference.  

- **`GetElementsValues()`**  
  Returns a dictionary of element values and ranges.  

- **`CreateElement(source, parameter, dataSource='parameter', customName=None)`**  
  Creates and binds a new UI element linked to a parameter or preset.  
  Handles the correct UI type allocation, binding, and reference registration.  

- **`AddScript()`**  
  Creates a special script element that executes custom code when triggered.  

- **`ClearParameters()`**  
  Removes all UI parameters after confirmation.  

- **`ResetParameters()`**  
  Resets all UI elements to their default stored values.  

- **`RewritePresetsOrder()`**  
  Updates preset button labels to match the internal preset manager order.  

- **`RenamePresetsOrder()`**  
  Renames and reorders presets based on current UI order.  

- **`ExpertMode(value)`**  
  Enables or disables “Expert Mode” for advanced control settings.  

---

### Preset Management

- **`ExportPresetsJSON()`**  
  Exports all presets, bindings, and element data to a `.json` file.  
  Used for saving full configuration states including UI bindings.  

- **`ExportPresetManager()`**  
  Creates a copy of the internal `PresetManager` for standalone use.  

- **`ImportPresetsJSON()`**  
  Imports presets and bindings from a `.json` file, reconstructing the UI and restoring order.  

- **`ClearPresets(overwriteWarning=True)`**  
  Clears all presets in both macro and micro (local) managers.  

---

### Randomization and Morphing

- **`SyncClocks()`**  
  Synchronizes morph timers across all linked elements.  

- **`SetRandom(mode=None)`**  
  Randomizes parameter values globally or per element.  

- **`MorphRandom(mode=None)`**  
  Performs a morph transition toward randomized target values.  

---

### Sequence Control

- **`PresetsSequence(sortKeys=False, keysSequence=None)`**  
  Traverses presets sequentially across all linked elements.  

- **`SequencePresets()`**  
  Executes a preset sequence defined by the order in the UI buttons.  

---

### Utility and Miscellaneous

- **`Interpolation`** *(property)*  
  Gets or sets the interpolation curve used for morphing.  

- **`Distribution`** *(property)*  
  Gets or sets the random distribution type.  

- **`GlobalTime`** *(property)*  
  Toggles global vs local morph timing control.  

- **`Automorph` / `Automorphs`** *(property)*  
  Controls automatic morph playback and its count.  

- **`Time`** *(property)*  
  Gets or sets the morphing duration.  

- **`NumberOfPresets`** *(property)*  
  Gets or sets the total number of available presets.  

- **`StorePreset(slot)`**  
  Stores the current preset into a numbered slot.  

- **`SetPreset(slot)`**  
  Loads and activates a stored preset.  

- **`DeletePreset(slot)`**  
  Deletes a stored preset by index.  

- **`GetElement(elementNum)`**  
  Returns a specific UI element by its numeric order.  

- **`Freeze(value)`**  
  Locks or unlocks the entire UI, preventing accidental changes.  

---

## Callbacks

The following methods execute when connected callback scripts are defined:

- **`OnMorphingStart(manager, morphingType, presetName)`**  
  Triggered when a morphing process starts.

- **`OnMorphingEnd(manager, morphingType, presetName)`**  
  Triggered when a morphing process ends.

- **`OnPresetCall(manager, morphingType, presetName)`**  
  Triggered when a preset is invoked manually or programmatically.

All callback functions look for an external module defined in  
`Elementscontainercallbacks` and call corresponding `onMorphingStart`,  
`onMorphingEnd`, or `onPresetCall` functions.

---

## Design Philosophy

- **UI-Driven Logic:** Designed for dynamic UI creation and interaction with parameters.  
- **Modularity:** Each container acts independently but can synchronize with others.  
- **Non-Destructive:** Parameters can be freely created, rebound, or deleted. 
- **Automation-Friendly:** Supports scripting, callback hooks, and sequenced morphing.  
- **MVC Compliance:** Acts as a **Controller** in the TDMorph architecture, linking UI (View) and PresetManager (Model).

---

## Dependencies

### TouchDesigner Components
- `PresetManager`
- `PresetMorpher`
- `Menus`
- `Elements`
- `Parameters`
- `TDResources`
- `Lib/Elements/*`

### Python Libraries
- `TDStoreTools.StorageManager`
- `json`

---
