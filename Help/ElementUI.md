# ElementUI 

## UI-level Methods

```python
SetUIElementValue()
```
Sets the element to the given value.

```python
ClickUIElementRandomize()
```
Trigger a randomization.

```python
ClickUIElementInterpolate()
```
Trigger a random interpolation.

```python
SetUIElementLock()
```
Lock the element.

```python
SetUIElementReveal()
```
Show all functions.

```python
ClickUIElementDestroy()
```
Destroy the element.

```python
SetUIElementDistribution()
```
Change the random distribution.

```python
SetUIElementInterpolation()
```
Change the interpolation curve.

```python
SetUIElementTime()
```
Change the interpolation curve.

```python
SetUISnap()
```
Chnage the snapping action.

```python
SetUIElementRange()
```
Change the range of the element.

```python
SetUIElementSignalEnable()
```
Enable/Disable the signal control.

```python
SetUIElementSignalSource()
```
Select the signal type.

```python
SetUIElementSyncMode()
```
Select the syncing mode.

```python
ClickUIElementManualTrigger()
```
Trigger a manual syncing.

```python
SetUIElementBeatFactor()
```
Change the factor for the syncing to occur as beats.

```python
SetUIElementBarFactor()
```
Change the factor for the syncing to occur as bars.

```python
SetUIElementPseq(sequence=[0.25, 0.5, 1.0])
```
Sets the sequence for the Pseq pattern.

```python
SetUIElementPrand(sequence=[0.25, 0.5, 1.0])
```
Sets the sequence for the Prand pattern.

```python
SetUIElementPxrand(sequence=[0.25, 0.5, 1.0])
```
Sets the sequence for the Pxrand pattern.

```python
SetUIElementPshuffle(sequence=[0.25, 0.5, 1.0])
```
Sets the sequence for the Pshuffle pattern.

```python
SetUIElementPwrandsequence=[0.25, 0.5, 1.0], weights=[0.33, 0.33, 0.33])
```
Sets the sequence and weights for the Pwrand pattern.


```python
SetUIElementPseries(start, step=1, length=10)
```
Sets the start, step and length for the Pseries pattern.


```python
SetUIElementPgeom(start, grow=1, length=10)
```
Sets the start, grow and length for the Pgeom pattern.

```python
SetUIElementPwhite(lo=0.0, hi=1.0)
```
Sets the lo and hi boundaries for the Pwthite pattern.


```python
SetUIElementPbrown(lo=0.0, hi=0.0, step=0.01)
```
Sets the lo, hi and step for the Pbrown pattern.


## Core-level properties

```python
Name()
```
Get/set stored element name.

```python
Interpolatable()
```
Get/set interpolation capability of element.

```python
Range()
```
Get/set stored range for element.

```python
LockStatus()
```
Get/set locked status.

```python
Value()
```
Get/Set element's value

## Core-level Methods
