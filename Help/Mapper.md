
# Mapper

## Core level methods

### Promoted

```python
ClearMappings()
```
Delete all exisitng presets from storage.

```python
ManageMappings()
```
Manage curent mappings from a table.

```python
Map(chanName)
```
Assing a MIDI control to an element.

```python
Parse(chanName, val, remapRange=None)
```
Does the actual MIDI to slider parsing. If remapRange passed, transforms 0-127 to given range.

```python
RecreateMappings()
```
This method recreates the mapping table. It is done in this way so we provide an interface to the user that can be used to delete and create new Mappings.

```python
ResetNumberOfMappings()
```
Reset the mappings count to current.

```python
SetActiveListener(active, path)
```
Route calls from sliders one by one, so that we can implement the "auto learn function".

```python
WriteMappingsTable()
```
Write the table where all mappings can be edited from.

## UI level methods

```python
getMappings()
```
Returns the mappings dependable dictionary.

```python
getNumberOfMappings()
```
Returns the number of currently stored mappings.

```python
getElementName(path)
```
Acquire the name of the mapped element.

```python
openAllChannels()
```
Allow for all channels to pass for parsing.
