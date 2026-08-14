# Element UI

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
ClickUIElementInterpolate()
```

```python
ClickUIElementManualTrigger()
```

```python
ClickUIElementRandomize()
```

```python
SetUIElementBarFactor(int)
```

```python
SetUIElementBeatFactor(int)
```

```python
SetUIElementDistribution(str)
```

```python
SetUIElementInterpolation(str)
```

```python
SetUIElementLock(bool)
```

```python
SetUIElementPbrown(lo=0.0, hi=1.0, step=0.01)
```

```python
SetUIElementPgeom(start, grow=2, length=10)
```

```python
SetUIElementPrand(sequence=[0.25, 0.5, 1.0])
```

```python
SetUIElementPseq(sequence=[0.25, 0.5, 1.0])
```

```python
SetUIElementPseries(start, step=1, length=10)
```

```python
SetUIElementPshuffle(sequence=[0.25, 0.5, 1.0])
```

```python
SetUIElementPwhite(lo=0.0, hi=1.0)
```

```python
SetUIElementPwrand(sequence=[0.25, 0.5, 1.0], weights=[0.33, 0.33, 0.33])
```

```python
SetUIElementPxrand(sequence=[0.25, 0.5, 1.0])
```

```python
SetUIElementRange(minVal, maxVal)
```

```python
SetUIElementReveal()
```

```python
SetUIElementSignalEnable()
```

```python
SetUIElementSignalSource(source='LFO')
```

```python
SetUIElementSyncMode(mode='Internal')
```

```python
SetUIElementTime(float)
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
getUIWidgetCheckbox(name)
```
Returns checkbox with given name.

```python
setUIWidgetValue(name, float)
```
Sets given widget with value.
