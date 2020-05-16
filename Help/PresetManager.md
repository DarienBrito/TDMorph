# Preset Manager

This is the heart of TDMorph. This class is in charge of executing and manage all presets storage and retrieval as well as 
communicating with the morpher and random distribution nodes.

## Properties

```python
AutoMode = bool
```
Changes the behaviour of "randomize" and "morph" to be automatic, based on an N number of morphs.

```python
LockedStatus = bool
```
Locks or opens the manager for randomization or morphing.

```python
CurrentPresetName = str
```
The currently selected preset. Used only as information, it does not set the preset.

```python
CurrentMorphCounter = int
```
The current morphing when automatic morphing is used.

### Wrappers

```python
NumMorphs()
```
The amount of morphings to occur in the inner PresetMorpher object.

```python
RandomDistribution()
```
The random distribution used in the inner PresetMorpher object.

```python
MorphTime()
```
The morphing time in the PresetMorpher inner object.

```python
MorphCurve()
```
The morphing curve used in the PresetMorpher inner object.

```python
ActivityStatus()
```
The idle/busy state of the PresetMorpher inner object.

```python
MorphingType() (read only)
```
The type of morpher used in the inner PresetMorpher object. 

```python
Blend = bool
```
Amount of blending in the inner PresetMorpher object.

```python
BlendingActive()
```
Blending status in the inner PresetMorpher object.

## Core level Methods

```python
GetEssentialStates()
```
Go over all target operators and get their essential states for morphing.

```python
GetStates()
```
Go over all target operators and get their states, including range, morph, time, etc information.

```python
GetElementsPaths()
```
Returns paths to all objects associated with the manager.

```python
GetStoredPresetsNum()
```
Returns the amount of stored presets.

```python
GetSavedStatesKeys()
```
Returns the names of the presets.

```python
GetPresetsDictionary()
```
Returns the presets dictionary (dependable dict, use .getRaw() to get normal dict from it)

```python
UpdatePresetsMenu()
```
This function gets called inside Preset manager every time there is a change in the dependable Presets dictionary. 

```python
StorePreset(name=str)
```
Stores a preset with the given name.

```python
StorePresetWithData(name=str, data=dict)
```
Stores a preset in the local storage of this component. It does so with given data, unlike the StorePreset method,
which grabs current parameters state.

```python
GetPreset(name=str)
```
Returns a specific preset as a list of lists of python dicts. 

```python
JumpToPreset(name=str)
```
Move to the specified preset immediately (no interpolation).

```python
DeletePreset(name=str)
```
Delete the specified preset.

```python
ClearPresets()
```
Destroys all stored presets.

```python
OverwritePresetsValue(element=str, parameter=str, item=str, val=float/int)
```
Used to overwrite a specific item in the parameter list. Will overwrite the given value for all presets.

```python
OverwriteSinglePresetValue(name=str, item=str, val=float/int)
```
Used to overwrite a specific preset's value. Will overwrite the value for all parameters only in that preset.

```python
AddDataToPreset(presetName=str, group=int, item=int, dataName=str, data=dict)
```
This method is to allow the addition of data points that are not supported in the core version of the PresetManager.
This is for example data from UI components, suchs LFO rate. Notice that the valid data structure for presets is:
		
```(DependableDict)(list)(list)(dict) = data```
```Presets[presetName][group][items][key] = data```

```python
GetMorphCurvesNames()
```
Returns all available morphing curve names.

```python
StopMorphing()
```
Stops the morphing clock.

```python
PlayMorphing(play=bool)
```
Play/Pauses the morphing clock.

```python
GeneratePresetsJSON()
```
Export all stored presets to a JSON file in disk

```python
ImportPresets()
```
Imports preset from a JSON file in disk. Files for this object must not contain bindings information (UI less).

```python
InjectPresets(data=dict)
```
This method can be used to inject data from a compound file, for instance with bindings information. 

## Wrappers

```python
SetPreset(presetName=str, morphTime=int)
```
Sets the speficied preset. Calls the same method in the inner PresetMorpher.

```python
Randomize(mode=str) # modes can be "Uniform", "Normal", "Beta"
```
Performs a randomization of parameters with given mode. Calls the same method in the inner PresetMorpher.

```python
RandomMorph(mode=str)  # modes can be "Uniform", "Normal", "Beta"
```
Performs a random morph of parameters. Calls the same method in the inner PresetMorpher.

```python
PresetsSequence(sortKeys=bool, keysSequence=list)
```
Performs the sequence of store presets. Calls the same method in the inner PresetMorpher. If a keys sequence is provided
it will perform the sequence in the order of the list. If sort keys is true, it will perform the sequence in the order
of the sorted keys.

```python
SetBlendingPresets(presetName=str, targetName=str)
```
Sets the blending for the specified presets. Calls the same method in the inner PresetMorpher.

```python
RandomizeParameter(name=str)
```
Randomizes the specified parameter only. Calls the same method in the inner PresetMorpher.

```python
MorphParameter(name=str)
```
Morphs the specified parameter only. Calls the same method in the inner PresetMorpher.
