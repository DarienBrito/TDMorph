# ParameterMorpher

## Core Methods
- **`GetContainer(n)`**  
  Retrieves a specific container UI by index.

- **`CreateContainer()`**  
  Creates a new container for slider-based UI elements.

- **`ExposeTimers(x=0, y=0)`**  
  Creates a new component that exposes all Preset Manager timers.

- **`ExposeChannels(x=0, y=0)`**  
  Creates a new component that exposes all parameter channels from sliders.

- **`ChangeOrientation(horizontal=False)`**  
  Changes the layout orientation of UI containers (if more than one) between horizontal and vertical modes.


## ElementsContainer

| **Property**        | **Type** | **Description**                                                                 |
|----------------------|----------|---------------------------------------------------------------------------------|
| `BindedPaths`        | `dict`   | Stores references to parameter bindings between UI elements and operators.      |
| `containerName`      | `str`    | Name assigned to this container instance.                                       |
| `NumberOfElements`   | `int`    | Number of UI elements within this container.                                   |
| `GlobalStatus`       | `bool`   | Whether operations (like morphing/randomization) are global or per-element.    |

## Public Methods

### UI and Binding Management

- **`CreateElement(source, parameter, dataSource='parameter', customName=None)`**  
  Creates and binds a UI element (slider, toggle, etc.) to a parameter or preset value.

- **`AddScript()`**  
  Creates a special script-based UI element that executes custom code on snap actions.

- **`ClearParameters()`**  
  Asks for confirmation, then deletes all parameters and associated UI elements.

- **`ResetParameters()`**  
  Restores all elements to their initial “drop-time” values.

- **`ExpertMode(value)`**  
  Enables or disables “expert mode,” showing advanced settings for experienced users.

- **`Freeze(value)`**  
  Freezes all UI elements to prevent accidental changes without affecting preset data.

---

### Preset Operations

- **`GetPresetManager()`**  
  Returns the internal `PresetManager` associated with this container.

- **`GetElementsValues()`**  
  Returns a dictionary containing the current values and ranges of all elements.

- **`ChangePresetsNum(newVal)`**  
  Increases or decreases the number of available presets.

- **`StorePreset(slot)`**  
  Stores the current parameter state into a numeric preset slot.

- **`SetPreset(slot)`**  
  Sets the container’s parameters to a stored preset.

- **`DeletePreset(slot)`**  
  Removes a preset from the preset manager.

- **`RewritePresetsOrder()`**  
  Updates button labels and internal preset numbering after renaming or reordering.

- **`RenamePresetsOrder()`**  
  Renames presets based on their visual order in the UI.

- **`SequencePresets()`**  
  Plays presets in sequence according to the current preset order.

---

### Export and Import

- **`ExportPresetsJSON()`**  
  Exports all presets, bindings, and UI order to a JSON file.

- **`ExportPresetManager()`**  
  Creates a copy of the local `PresetManager` on the root TDMorph level for independent use.

- **`ImportPresetsJSON()`**  
  Imports presets and bindings from a previously exported JSON file, rebuilding UI elements.

- **`ClearPresets(overwriteWarning=True)`**  
  Clears all stored presets, both global and local to each UI element.

---

### Global and Randomization Controls

- **`SyncClocks()`**  
  Synchronizes morph clocks across all elements.

- **`SetRandom(mode=None)`**  
  Applies randomization either globally or per element, depending on `GlobalStatus`.

- **`MorphRandom(mode=None)`**  
  Performs morphing between random parameter values.

- **`PresetsSequence(sortKeys=False, keysSequence=None)`**  
  Traverses presets in order, either globally or locally per element.

---

### Utility and System Methods

- **`UpdateSize(sizeLimit=720)`**  
  Resizes the container to fit all elements, up to a specified limit.

- **`HardSyncLFOs()`**  
  Resets all LFOs in the UI to their initial phase.

- **`GetBindedKeys()`**  
  Returns all parameter binding identifiers in the container.

- **`GetElement(elementNum)`**  
  Returns a specific UI element by its index (starting from 1).

- **`Name`** *(property)*  
  Gets or sets the container’s name.

- **`Interpolation`, `Distribution`, `Automorph`, `Automorphs`, `Time`, `NumberOfPresets`**  
  Linked getters/setters for internal `PresetManager` parameters.

- **`GlobalTime`** *(property)*  
  Toggles global morph/randomization mode for this container.
