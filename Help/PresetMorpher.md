# Preset Morpher

## Properties

```python
NumMorphs = int
```
Amount of morphings

```python
RandomDistribution = str
```
Get/set random distribution

```python
MorphTime = float
```
Get/set morph time  

```python
MorphCurve = str
```
Get/set morph curve

```python
ActivityStatus = bool (read only) 
```
Returns true if morpher is active

```python
MorphingType = str (read only)
```
Return current morphing type. This can be:

  * Autorand
  * Automorph
  * Autopresets
  * None

```python
BlendingActive = bool 
```
Get/Set blending behaviour

```python
Blend = float
```
Get/Set blending factor

## Core level methods

``` python
UpdateTables()
```
This method updates the target tables so that values are properly in sync. Typically this method will be called when on completion of a timer.

```python
SetPreset(presetName, overrideTypeFlag=False, morphTime=None)
```
Sets a preset with an arbitrary name. If morphTime is passed, then stored preset time is ignored and passed value is used instead.

```python
SetSpecialValues()
```
Sets non-interpolatable values to given state.

```python
SetCuedSpecialValues()
```
Executes the special parameters that were saved for "end" interpolation execution.

```python
Refresh(timerActive=False)
```
Update tables here to make sure order of execution is correct and disable clock, to make sure nothing cooks when idle.

```python
Randomize(mode=None)
```
Move to a random state GLOBALLY.

```python
RandomMorph(mode=None)
```
Morph to a random state GLOBALLY

```python
RandomizeGivenParameters(operatorIndex, names, mode=None)
```
Randomize specific parameters only. 

``` python
MorphGivenParameters(operatorIndex, names, mode=None)
```
Morph specific parameters only.

```python
AutoRandomize(mode=None)
```
Move to N random states jumping.

```python
AutoRandomMorph(mode=None)
```
Move to N random states using morphing.

```python
PresetsSequence(sortKeys=False, keysSequence=None)
```
Move across all stored presets. One can pass the keys in an arbitrary order if wanted. If no keys are passed, then the sequence is played in the 
order on which the items were entered.

```python
SetBlendingPresets(presetName, targetName)
```
Allows for arbitrary blending between two presets.

## UI level methods

```python
RandomizeWithStoredRanges(mode=None)
```
Move to a random state GLOBALLY, using a define set of ranges (useful for dynamic UI's)
    
```python
RandomMorphWithStoredRanges(mode=None)
```
Move to a random state using morphing GLOBALLY using a defined set of ranges (useful for dynamic UI's)

```python
AutoRandomizeWithStoredRanges(mode=None)
```
Move to N random states jumping, using the ranges from the UI.

```python
AutoRandomMorphWithStoredRanges(mode=None)
```
Move to N random states using morphing, using the ranges from the UI
