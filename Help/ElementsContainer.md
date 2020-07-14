# ElementsContainer 

## Core-level methods

### Properties

```python
Name = str
```
Get/set container name

### Promoted

```python
AddBindingReference(source, bindedData, elementPath, customName=None)
```
Stores useful references from all created bindings, so that later on we can use our presets. It stores this properties in a unique name that I call "cross-check name", which is used first to see if a parameter already exists in TDMorph. This is there because otherwise it would be possible to create two elements for the exact same parameter. Different nodes could also have the same paramter name, so we need the whole path as a key to discern from where we are grabbing data.

```python
AddScript()
```
Scripts are a special type of elements that execute on the given snap action.

```python
BindingsTableEdited()
```
Recreates the bindings table based on the edits from user.

```python
ChangePresetsNum(newVal)
```
Sets the number of presets in the Elements container to newVal.

```python
ClearParameters()
```
Deletes all elements in the ElementsContainer.

```python
CreateElement(source, parameter, dataSource='parameter', customName=None)
```
Handles UI creation from a stored preset or from a grabbed parameter. In here operations for correct UI resource allocation take place. Notice that we recreate the original data type for each UI element, to make the most out of the limitations	with cloning, which do not allow for a full Object Oriented approach.

```python
Delete()
```
Deletes the ElementsContainer.

```python
ExportPresetManager()
```
Creates a copy of the local preset manager on the level of TDMorph for independent use, for instance with a preset composer or animator.

```python
ExportPresetsJSON()
```
Export all stored presets to a JSON file in disk. Notice that this is a special method of SlidersContainer, since it can have bindings. The method from PresetManager is different, and does not contain binding information.

```python
GetBindedKeys()
```
Returns the keys in the bindings deeply dependable dictionary.

```python
GetElementsValues()
```
Returns the elements properties as a dictionary o name: value, range

```python
GetPresetManager()
```
Returns the internal preset manager for this ElementsContainer.

```python
HardSyncLFOs()
```
Resyncs all LFO's in the inner elements of the ElementsContainer.

```python
ImportPresetsJSON()
```
Import stored presets to a JSON file in disk. Notice that this is a special method of ElementsContainer, since it can have bindings. The method from PresetManager is different, and does not contain bindings information.

```python
OpenBindingsTable()
```
Invoke table with all written bindings.

```python
RenamePresetsOrder()
```
Renames the found presets in the order which they visually have.

```python
ReportResult()
```
Invokes a pop-up window that displays msg and title.

```python
ResetParameters()
```
Reset all elements to the values found on drop in the ElementsContainer.

```python
RewritePresetsOrder()
```
Updates the labels in the buttons to the changed order/naming in the preset manager. Handy for when writing to the internal preset manager from outside, like with the SceneLauncher. 

```python
UpdateSize()
```
Re-scale based on elements content.

```python
WriteBindingsTable()
```
Writes a table with all current binding so the user can access an edit the data in a comfortable way.

### Private

```python
constructBindingPackage(ccName, data)
```
Very low level method that assembles a dictionary compatible with TDMorphs binding system.

```python
correctParameterType(element, uielement)
```
This function makes sure that the widget that we choose has the right parameter type. PresetManager looks at that parameter to come up with the right mapping, hence we need to parse this accordingly.

```python
createUIElement(parameter, dataSource, style=None)
```
This function allocates a particular UI from this lookup dictionary. All these are UI components that live in the UI library of TDMorph.

```python
deleteElements()
```
Unbind and destroy all elements.

```python
getElementsOrder()
```
Find the order on which the elements are placed in the UI.

```python
getElementsPaths()
```
Gathers all e;ements in this ElementsContainer.

```python
reBind(slider, target, name, style)
```
Rebind passed slider to target, this is used when editing a bindings table.

## UI-level methods

All following methods set the elements on the UI level. These should be self explanatory if not described.

### Promoted

```python
ClickUIAddPreset()
```

```python
ClickUIClearPresets()
```

```python
ClickUIMorph()
```

```python
ClickUIRandomize()
```

```python
ClickUISequence()
```

```python
ClickUISubPreset()
```

```python
ClickUISync()
```

```python
ExpertMode(enable=False)
```
Enables advanced features for users that are already proficient with TDMoprh. Henece "expert" mode.

```python
GetElement(elementNum)
```
Returns element in position elementNum in ElementsContainer.

```python
SetUIAuto(False)
```
Sets automatic random and morphing status for the ElementsContainer.

```python
SetUIDistribution(str)
```
Sets the random distribution in the UI element.

```python
SetUIGlobal(bool)
```
Sets the global status in the UI element.

```python
SetUIHardSyncLFOs()
```
Hard syncs LFO's in the Container from the UI level.

```python
SetUIInterpolation(str)
```
Sets the morphing curve in the UI element.

```python
SetUIMorphs(int)
```
Sets the number of automatic morphs that should take place.

```python
SetUINumPresets(int)
```
Sets number of preset slots available.

```python
SetUISetPreset(int)
```
Sets the targetted preset from the UI level.

```python
SetUIStorePreset(int)
```
Stores the targetted preset from the UI level.

```python
SetUITime(float)
```
Sets the targetted time from the UI level.

```python
SetUIUnstorePreset(int)
```
Unstores the targetted preset from the UI level.

```python
UIExportPresets()
```
Exports presets to JSON.

```python
UIFreezeState()
```
Freezes the sliders in the current state, so that editing cannot happen by accident. This method does nothing to the presets themselves, it simply disables interaction with the elements.

```python
UIImportPresets()
```
Import presets to JSON.

### Private

```python
clickUIWidgetButton()
```
Clicks UI with given name. "name" is a local alias defined in the class.

```python
getUIElement()
```
Returns UI with given name. "name" is a local alias defined in the class.

```python
getUIWidgetCheckbox()
```
Clicks checkbox with given name. "name" is a local alias defined in the class.

```python
setUIWidgetValue()
```
Supports for Widget's and TDMorph's buttons. Any controller added to TDMorph's internal widgets has to have "Value" or "Value0" as name for its main parameter, otherwise it will not be able to perform all features.
