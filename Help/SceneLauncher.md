# SceneLauncher

## Core level methods

### Properties (read/write)

```python
Source = v
```
v is a preset manager

```python
Row = v
```
v is current row

```python
Col = v
```
v is current col

```python
Scene = v
```
v is current scene

```python
Target = v
```
v is current target

### Promoted

```python
ClearActions()
```
Clear all actions listed in the Scene launcher.

```python
CreateScene(name, target='None')
```
Create a new Scene with optional target.

```python
DelayedPresetTrigger(target, length, curve)
```
Trigger a preset with a delay.

```python
DuplicatePreset(name, target)
```
Duplicate target preset.

```python
DuplicateScene(name, sourceName)
```
Duplicate sourceName scene with given name.


```python
EnableFollowActions(enable=True)
```
Activate/Deactive follow actions functionality.

```python
EnableScripting(enable=True)
```
Activate/Deactive scripting possibilities in the launcher.

```python
ExportPresetsJSON()
```
Export current presets including scenes to disk.

```python
GetCueActions()
```
Grab available morph curves from source.

```python
GetCurrentCellValue(cellName)
```
Grab acurrent cellName data.

```python
GetMorphCurves()
```
Grab available morph curves from source.

```python
ImportPresetsJSON()
```
Import presets including scenes from disk. 

```python
PerformAction(action, value=None)
```
Trigger some action from the transport menu. Value is only useful for Play/Pause action.

```python
ReportResult(msg, title)
```
Creates a TDMorph-formatted pop-up window with given message and title.

```python
SequentialLaunch(data)
```
This is a special method used exclusively by the "Sequence" action. See SceneLauncher/Actions to understand the logic.

```python
SetCellColor()
```
Overlay color for lister's cells.

```python
SetLengthMode()
```
This sets the time according to a define time unit, this can be seconds, sixteenths, beats or bars.

```python
WritePresets()
```
Write the found presets into the table in this component. This gets recalled automaticall everytime the presets changed.

```python
WriteScenes()
```
Write the found scenes into the table in this component. This gets recalled automatically everytime the scenes changed.

### Private

```python
assembleLaunchInfo()
```
Manually recreate a minimal info dictionary to be used with the lister callbacks.

```python
getRandomColor()
```
Returns a random color for the cells.

```python
launchCell(row)
```
Triggers the "Launch" cell at given row.

```python
onAny()
```
Execute homonimus action.

```python
onFirst()
```
Execute homonimus action.

```python
onLast()
```
Execute homonimus action.

```python
onNext(info, isSequence=False)
```
Execute homonimus action. info is lister callback info object. If sequence then continues until no cells left.

```python
onOther(info)
```
Execute homonimus action. info is lister callback info object.

```python
onPlayPause(info, value)
```
Execute homonimus action. info is lister callback info object. value is on or off.

```python
onPrevious(info)
```
Execute homonimus action. info is lister callback info object.

```python
onRepeat(info)
```
Execute homonimus action. info is lister callback info object.

```python
onSequence()
```
On sequence plays the whole scenes sequence, ignoring the actions column. This is handled in the actions callback.

```python
onStop(info)
```
Execute homonimus action.

```python
selectRow(row)
```
Note that when this gets executed, the onSelectRow() callback inside the lister is activated, so we update there the currently selected row for the SceneLauncher.

```python
updateTimeInfo(totalDuration)
```
Updates the COMP with total duration calculated from the sum of all scenes, including delays.

## UI level methods

### Promoted

```python
CreateAnimation()
```
Creates an animation from the set of scenes in the SceneLauncher.

### Private

```python
createAnimationCOMP( x=250, y=0, viewer=True)
```
Creates a copy of the requested item on the location  of TDMorph. Possible objects are:PresetManager, PresetsGrabber, PresetsAnimator

