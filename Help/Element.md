This is the prototype class for all local Elements, which are based on TDMorphs' Widgets, which are:

1. TDMorphFloat
1. TDMorphButton
1. TDMorphCheckbox
1. TDMorphButtonPopUp
1. TDMorphSlider
1. TDMorphToggle
1. TDMorphMenu
1. TDMorphField
1. TDMorphStringMenu

Each one of this has slight variations of this prototype class to fit their local types. The properties here defined are mainly used by the OSC and MIDI Mappers. The prototype is defined as follows:

## Core level methods

### Properties

```python
Name (read only)
```
Get the Element's internal name

```python
Value = float
```
Get/Set the Element's value

```python
Range = (float, float)
```
Get/Set the Element's internal range

### Promoted

```python
OffToOn()
```
Off to on script execution.

```python
OnToOff()
```
On to off script execution.

```python
OnValueChange()
```
On value change script execution.
