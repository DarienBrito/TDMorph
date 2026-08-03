
# Mapper

> **PROPRIETARY. Licensed, not sold.** Part of the commercial ParameterMorpher and
> SceneLauncher components, available through
> [Patreon](https://www.patreon.com/c/darienbrito), not from this repository.

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
SetActiveListener(active, path)
```
Route calls from sliders one by one, so that we can implement the "auto learn function".

## UI level methods

```python
Mappings()
```
Returns the mappings dependable dictionary.

```python
NumberOfMappings()
```
Returns the number of currently stored mappings.
