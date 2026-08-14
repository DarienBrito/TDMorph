# Preset Manager

The heart of TDMorph. This class is in charge of executing and manage all presets storage and retrieval as well as 
communicating with the morpher and random distribution nodes.

## Core level methods

### Properties

```python
AutoMode = bool
```
Changes the behaviour of "randomize" and "morph" to be automatic, based on an N number of morphs.

```python
CurrentMorphCounter = int
```
The current morphing when automatic morphing is used.

```python
CurrentPresetName = str
```
The currently selected preset. Used only as information, it does not set the preset.

```python
LockedStatus = bool
```
Locks or opens the manager for randomization or morphing.

### Promoted

```python
AddDataToPreset(presetName, group, item, dataName, data)
```
This method is to allow the addition of data points that are not supported in the core version of the PresetManager.
This is for example data from UI components, suchs LFO rate. Notice that the valid data structure for presets is:
		
```(DependableDict)(list)(list)(dict) = data```
```Presets[presetName][group][items][key] = data```

```python
ClearPresets()
```
Destroys all stored presets.

```python
DeletePreset(name=None)
```
Delete the specified preset. If no name is supplied the one found in the custom parameters of PresetManager will be used.

```python
GeneratePresetsJSON()
```
Export all stored presets to a JSON file in disk

```python
GetElementsPaths()
```
Returns paths to all objects associated with the manager.

```python
GetEssentialStates()
```
Go over all target operators and get their essential states for morphing.

```python
GetEssentialStatesFromParameters()
```
This is used when one wants to target specifc parameters from specific operators in morphing.

```python
GetMorphCurvesNames()
```
Returns all available morphing curve names.

```python
GetPreset(name) 
```
Returns a specific preset as a list of lists of python dicts.

```python
GetPresetsDictionary()
```
Returns the presets dictionary (dependable dict, use .getRaw() to get normal dict from it)

```python
GetRandomDistributionNames()
```
Returns the possible names for random distributions.

```python
GetSavedStatesKeys()
```
Returns the names of the presets.

```python
GetStates()
```
Go over all target operators and get their states, including range, morph, time, etc information.

```python
GetStatesFromParameters(parameters)
```
This is used when one wants to target specifc parameters from specific operators in randomization.

```python
GetStoredPresetsNum()
```
Returns the amount of stored presets

```python
ImportPresets()
```
Imports preset from a JSON file in disk. Files for this object must not contain bindings information (UI less).

```python
InjectPresets(data)
```
This method can be used to inject data from a compound file, for instance with bindings information. 

```python
JumpToPreset(name=None)
```
Move to the specified preset immediately (no interpolation). If no name is supplied the one found in the custom parameters of PresetManager will be used.

```python
MorphGivenParameters(operatorIndex, names, mode=str)
```
Morphs the specified parameters only. First argument is the row index from the table with supplied operators paths. Names are the names of the targeted parameters. Mode is random type. Uses the current one if not specified.

```python
OverwritePresetsValue(element, parameter, item, val)
```
Used to overwrite a specific item in the parameter list. Will overwrite the given value for all presets.

```python
OverwriteSinglePresetValue(name, item, val)
```
Used to overwrite a specific preset's value. Will overwrite the value for all parameters only in that preset.

```python
PlayMorphing(play=True)
```
Play/Pauses the morphing clock.

```python
PresetsSequence(sortKeys=False, keysSequence=None)
```
Performs the sequence of store presets. Calls the same method in the inner PresetMorpher. If a keys sequence is provided it will perform the sequence in the order of the list. If sort keys is true, it will perform the sequence in the order of the sorted keys.

```python
RandomMorph(mode='Uniform')
```
Performs a random morph of parameters. Calls the same method in the inner PresetMorpher.

```python
Randomize(mode=None)
```
Performs a randomization of parameters with given mode. Calls the same method in the inner PresetMorpher.

```python
RandomizeGivenParameters(operatorIndex, names, mode=None)
```
Randomizes the specified parameters only. First argument is the row index from the table with supplied operators paths. Names are the names of the targeted parameters. Mode is random type. Uses the current one if not specified.

```python
ReportResult(msg, title)
```
Launches a TDMorph-formatted pop up window with the given message and title.

```python
SetBlendingPresets(presetName, targetName)
```
Sets the blending for the specified presets. Calls the same method in the inner PresetMorpher.

```python
SetPreset(presetName, morphTime=1)
```
Sets the speficied preset. Calls the same method in the inner PresetMorpher.

```python
StopMorphing()
```
Stops the morphing clock.

```python
StorePreset(name='Preset0')
```
Stores a preset with the given name. If no name is supplied the one found in the custom parameters of PresetManager will be used.

```python
StorePresetWithData(name, data)
```
Stores a preset in the local storage of this component. It does so with given data, unlike the StorePreset method, which grabs current parameters state.

```python
UpdatePresetsMenu()
```
This function gets called inside Preset manager every time there is a change in the dependable Presets dictionary. 

## Private

```python
fitWildcard(pattern)
```
Add support for the ^ wildcard used in TD.

```python
getEsssentialState(target, parameters=None)
```
Grabs only essential elements to interpolate across tables.

```python
getLockFromUI(path)
```
Check if there's an embedded UI to get locked status from, otherwise grab the status from self.

```python
getParameterSelection(target, parsSelection, scope)
```
Parse parameters to returb based on pattern matching from the selected flags in the node.

```python
getParameterValue(parameter)
```
Grabs the source value based on certain conditions. There are some parameters, such as menu, that may require special treatment. This method is meant to handle that.

```python
getParams(target)
```
Filters the parameters to be selected based.

```python
getState(target, parameters=None)
```
Get the parameters current state. Takes useful information for morphing and parametric setting. We include here curve and time information.

```python
parseScope(pattern)
```
Add suport for multiple wildcard in parameter one liner, as in TD. i.e x* yy* zzz*.

```python
parseSelection()
```
Parsing of user input in relation to what parameters to grab from targeted operators.

## UI level methods

### Properties

```python
UIGlobalStatus = bool
```
Global is true, local false.

### Promoted

```python
UIAutoRandomLocal(mode=None)
```
Sets automatic randomization locally. Only works if there are associated Widgets.

```python
UIAutoRandomMorphLocal(mode=None)
```
Sets automatic morphing locally. Only works if there are associated Widgets.

```python
UIClearPresets()
```
Destroy all presets.

```python
UIGetCurveLabels()
```
Gets all names of curves.

```python
UIGetPresetValue(address, key)
```
Returns a specific presets time, reading from a list of lists of python dicts, stored in Presets. This is specific for UI usage.

```python
UIPresetsLocalSequence(sortKeys=False, keysSequence=None)
```
Sets the given presets sequence locally. Only works if there are associated Widgets.

```python
UIPresetsSequence(sortKeys=False, keysSequence=None)
```
Sequence parameters from the UI.

```python
UIRandomLocalMorph(mode=None)
```
Morphs the parameters with defined ranges in the UI.

```python
UIRandomMorph(mode=None)
```
Morph parameters from the UI.

```python
UIRandomize(mode=None)
```
Randomize parameters from the UI.

```python
UIRandomizeLocal(mode=None)
```
Randomizes the parameters with defined ranges in the UI.

```python
UISetPreset(presetName, morphTime=None)
```
Set specified preset from the UI.

```python
UISetPresetLocally(presetName)
```
Sets the given presets values locally. Only works if there are associated Widgets.

```python
UISetElementTime()
```
Sets the time via the UI, so that change is visible to the user. Only works if there's an associated element.

```python
UIStorePreset(name=None)
```
Stores a preset with the given name.

```python
UISyncClocks()
```
Syncs all the inner clocks in the Container.
