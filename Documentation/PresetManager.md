# Preset Manager

| **Property**          | **Type** | **Description**                                                                 |
|------------------------|----------|---------------------------------------------------------------------------------|
| `Presets`              | `dict`   | Dictionary of stored presets. Each preset contains parameter states, morph time, curve, and random distribution. |
| `AutoMode`             | `bool`   | Enables automatic randomization or morphing.                                   |
| `CurrentPresetName`    | `str`    | The currently selected preset name.                                            |
| `CurrentMorphCounter`  | `int`    | The current morph iteration count.                                             |
| `LoopSequenceStatus`   | `bool`   | Enables looping through preset sequences.                                      |
| `RandomDistribution`   | `str`    | The random distribution function used by the morpher.                          |
| `NumMorphs`            | `int`    | Number of morph steps per transition.                                          |
| `MorphTime`            | `float`  | Time (in seconds) for a morph transition.                                      |
| `MorphCurve`           | `str`    | Type of interpolation curve used.                                              |
| `Blend`                | `float`  | Blend factor for mixing presets.                                               |
| `BlendingActive`       | `bool`   | Indicates if blending between presets is active.                               |
| `Lock`                 | `bool`   | Prevents editing of presets when active.                                       |


## Core Methods

### Preset Storage and Retrieval
- **`StorePreset(name=None)`**  
  Creates a new preset from the current state of all linked operators.

- **`DeletePreset(name=None)`**  
  Removes a preset from memory.

- **`ClearPresets(overwriteWarning=False)`**  
  Deletes all presets, optionally skipping confirmation prompts.

- **`OverwriteCurrentPreset()`**  
  Replaces the currently selected preset with current parameter values.

---

### Preset Application and Morphing
- **`SetPreset(name=None)`**  
  Applies a preset immediately (without interpolation).

- **`MorphPreset(presetName, morphTime=None, morphCurve=None)`**  
  Smoothly interpolates parameters to the given preset using the specified curve and duration.

- **`StopMorphing()`**  
  Stops any ongoing morph process.

- **`PlayMorphing(play=True)`**  
  Starts or pauses morphing playback.

- **`PresetsSequence(sortKeys=False, keysSequence=None)`**  
  Plays a defined sequence of presets in order.

- **`SetBlendingPresets(presetName, targetName)`**  
  Sets up two presets to blend between.

---

### Randomization
- **`SetRandom(mode=None)`**  
  Applies random parameter values to all linked operators.

- **`MorphRandom(mode=None)`**  
  Interpolates between the current state and random values.

- **`RandomizeGivenParameters(operatorIndex, names, mode=None)`**  
  Randomizes a specific subset of parameters on a given operator.

- **`MorphGivenParameters(operatorIndex, names, mode=None)`**  
  Morphs a specific subset of parameters on a given operator.

---

### Import and Export
- **`ExportJSON()`**  
  Exports all presets to a JSON file via a save dialog.

- **`ImportJSON()`**  
  Imports presets from a JSON file.

- **`InjectPresets(presets)`**  
  Overwrites existing presets with an externally provided dictionary.


### Path and Preset Management
- **`GetPresetsKeys()`**  
  Returns a list of stored preset names.

- **`GetNumPresets()`**  
  Returns the total number of presets.

- **`GetMorphCurvesNames()`**  
  Lists available morph curves from the PresetMorpher.

- **`GetRandomDistributionNames()`**  
  Lists available random distribution types.

- **`GetElementsPaths()`**  
  Retrieves paths to all linked operator elements.

---
