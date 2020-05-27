# ElementsContainer 

## Properties

```python
Name(str)
```
The container name

## UI-level Methods

```python
SetUIDistribution(str)
```
Changes the random distribution (Uniform, Normal, Beta).

```python
SetUIInterpolation(str)   
```
Changes the moprhing curve (Linear, Scurve, etc).

```python
SetUIGlobal(bool) 
```
Enables local/global behaviour.

```python
ClickUISync()  
```
Enables local/global clock syncing.

```python
SetUIAuto(bool)    
```
Enables automatic behaviour.

```python
SetUIMorphs(int)      
```
Sets the amount of morphings.

```python
SetUITime(float)    
```
Sets the morphing time.

```python
ClickUISequence()   
```
Clicks the preset sequence button.

```python
ClickUIRandomize() 
```
Clicks the randomize button.

```python
ClickUIMorph()    
```
Clicks the morph button.

```python
UIImportPreset() 
```
Triggers importing a preset.

```python
UIExportPreset()    
```
Triggers exporting a preset.

```python
ClickUISubPreset()    
```
Substracts one preset slot.

```python
ClickUIAddPreset()      
```
Adds one preset slot.

```python
SetUINumPresets(int)  
```
Changes the number of preset slots.

```python
ClickUIClearPresets() 
```
Clears all presets.

```python
SetUISetPreset(int)  
```
Sets preset n.

```python
SetUIStorePreset(int)     
```
Stores a preset in n slot.

```python
SetUIUnstorePreset(int)   
```
Removes a preset from n slot.

```python
SetUIHardSyncLFOs
```
Hard-syncs all LFO's in the container.

```python
GetElement(int)   
```
Returns a widget from the container.

## Core level Methods

```python
Delete()
```
Destroys the container

```python
UpdateSize(sizeLimit=720)
```
Resizes the container so that it fits inner elements.

```python
HardSyncLFOs()
```
Sends a reset signal to all LFO's for all widgets in the container.

```python
ChangePresetsNum(int)
```
Sets the number of preset slots.

```python
GetBindedKeys()
```
Returns the stored keys for binded parameters

```python
GetPresetManager()
```
Returns the preset manager that lives in the container.

```python
WriteBindingsTable()
```
Updates an inner table with all current binding data, used so the user can access an edit the data in a comfortable way.

```python
OpenBindingsTable()
```
Invkoes the bindings table.

```python
AddBindingReference(source, bindedData, elementPath, customName=None)
```
Creates a reference for a given parameter.

```python
CreateElement(source, parameter, dataSource='parameter', customName=None)
```
Creates an element (widget) for the given parameter. Default data source is 'parameter', if not parameter thing it comes from a preset.

```python
ExportPresetsJSON()
```
Exports all stored presets to a JSON file in disk. Notice that this is a special method of SlidersContainer, since it can have bindings

```python
ExportPresetManager()
```
Creates a copy of the local preset manager on the level of TDMorph for independent use, for instance with a preset composer or animator.

```python
ImportPresetsJSON()
```
Import stored presets to a JSON file in disk. Notice that this is a special method of SlidersContainer, since it can have bindings


