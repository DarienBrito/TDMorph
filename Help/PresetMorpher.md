# Preset Morpher

## Core-level methods

# Properties

```python
ActivityStatus = bool (read only) 
```
Returns true if morpher is active

```python
BlendingActive = bool 
```
Get/Set blending behaviour

```python
Blend = float
```
Get/Set blending factor

```python
MorphCurve = str
```
Get/set morph curve

```python
MorphTime = float
```
Get/set morph time  

```python
MorphingType = str (read only)
```
Return current morphing type. This can be:

  * Autorand
  * Automorph
  * Autopresets
  * None
 
```python
NumMorphs = int
```
Amount of morphings

```python
RandomDistribution = str
```
Get/set random distribution 

### Promoted

```python
AutoRandomMorph(mode=None)
```
Move to N random states using morphing.

```python
AutoRandomize(mode=None)
```
Move to N random states jumping.

```python
MorphGivenParameters(operatorIndex, names, mode=None)
```
Morph specific parameters only.

```python
PresetsSequence(sortKeys=False, keysSequence=None)
```
Move across all stored presets. One can pass the keys in an arbitrary order if wanted. If no keys are passed, then the sequence is played in the 
order on which the items were entered.

```python
RandomMorph(mode=None)
```
Morph to a random state GLOBALLY.

```python
Randomize(mode=None)
```
Move to a random state GLOBALLY.

```python
RandomizeGivenParameters(operatorIndex, names, mode=None)
```
Randomize specific parameters only.

```python
Refresh(timerActive=False)
```
Update tables here to make sure order of execution is correct and disable clock, to make sure nothing cooks when idle.

```python
SetBlendingPresets(presetName, targetName)
```
Allows for arbitrary blending between two presets.

```python
SetCuedSpecialValues()
```
Executes the special parameters that were saved for "end" interpolation execution.

```python
SetCurrentPresetName(name)
```
Sets current morpher preset name to given one.

```python
SetPreset(presetName, overrideTypeFlag=False, morphTime=None, morphCurve=None)
```
Sets a preset with an arbitrary name. If morphTime is passed, then stored preset time is ignored and passed value is used instead.

```python
SetSpecialValues()
```
Sets non-interpolatable values to given state. Used only for preset setting, since one cannot have random transformation for str, ops, etc.

```python
UpdateTables()
```
This method updates the target tables so that values are properly in sync. Typically this method will be called when on completion of a timer.

### Private

```python
checkPresetCycle(funcOn, funcOff=None)
```
Keep track of inner morphing count and perform actions based on that count.

```python
enableInterpolation(enabled)
```
Enable/disable interpolation.

```python
getParameterValue(data, decimals=8)
```
Return a random value for the given parameter.

```python
getRandomValue(mode, minMax, paramType, decimals=8)
```
Gets random values with different distributions from the RandomGenerator module. Certain parameter types need only  certain values, such as two integer states, for instance.

```python
getStatesFromGivenParameters(operatorIndex, names, essential=False)
```
Get states only from the user specified operator by index from the operator finder and given parameter names.

```python
inferRandMode(mode)
```
Get a random mode from arg, if non exists, take the one set in the custom Parameters field. Mode is a str as 'uniform', 'normal' or 'beta'.

```python
keepCount(funcOn=None, funcOff=None)
```
Keep track of inner morphing count and perform actions based on that count.

```python
setAttributeParameterProperties(states, decimals=8)
```
Low level method to write parameters directly.

```python
setComputedParameterProperties(states, target=None, decimals=8)
```
Low level method to write computed parameters.

```python
setOriginalParameterProperties(states, target=None, decimals=8)
```
Low level method to write originatl parameters.

```python
setRandomVals(states=None)
```
Randomizes values using a defined random distribution. This method writes directly to the parameters. It is used by Randomize().

```python
setTimer(active=True, cycle=False, morphTime=None)
```
Sets the morphing timer to specified properties.

```python
signalCompletion()
```
Used to signal when the morphing is done. It flips the state of a constant so that the signal can be used to control things outside this node. I do not use a pulse because that will always cook. This cooks only once, when needed.

```python
writeEssentialValues(target, states=None)
```
Writes all found states if there are any to be found.

```python
writePresetToChannels(target, states)
```
Writes data for preset morphing in the tables. This method handles special parameters too, that get written in the "Special" table. Those are parameters that cannot be interpolated. This accounts exclusively for presets setting.

```python
writePresetValues(target, presetName, withSpecial=True)
```
Writes presets if there are values to be found.

```python
writeRandomVals(states=None)
```
Generates random values according to selected random distribution, in random morphing.

## UI-level methods

### Promoted

```python
AutoRandomMorphWithStoredRanges()
```

```python
AutoRandomizeWithStoredRanges()
```

```python
RandomMorphWithStoredRanges()
```

```python
RandomizeWithStoredRanges()
```

### Private

```python
getParameterValue()
```

```python
setAttributeParameterProperties()
```

```python
setComputedParameterProperties()
```

```python
setRandomValsWithStoredRanges()
```

```python
writeRandomValsWithStoredRanges()
```
