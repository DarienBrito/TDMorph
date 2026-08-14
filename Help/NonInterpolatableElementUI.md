# NonInterpolatableElementUI

## Core-level methods

### Promoted

```python
DestroyElement()
```
Destroys the Widget.

```python
EditCustomName(name)
```
Change the name of the slider in the custom entry (maintains original name intact).

```python
GetPresetsManager()
```
Returns the deply dependable dictionary that holds presets.

```python
GetRandomDistribution()
```
Returns current random distribution.

```python
HardSync()
```
Resync the LFO using a high level control.

```python
Reorder(name, source, receiver)
```
Reorder widgets.

```python
SetDefaultValue()
```
Set the slider to the range and value found on creation (original value on dragging of parameter).

```python
SetSliderDecimalPoints(val)
```
Sets the floating point precision for sliders.

### Private

## UI-level methods

All following methods set the elements on the UI level. These should be self explanatory.

### Promoted

```python
ClickUIElementDestroy()
```

```python
SetUIElementValue(float)
```

```python
SetUISnap(int)
```

### Private

```python
clickUIWidgetButton()
```

```python
getUIElement(name)
```
Returns element with given name.

```python
setUIWidgetValue(name, float)
```
Sets given widget with value.
