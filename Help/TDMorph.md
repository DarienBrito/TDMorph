# TDMorph 

## Methods

```python
ChangeOrientation(horizontal=False)
```
Changes the look of TDMorph from vertical to horizontal. Only useful if there is more than a single container in the Window.
  
```python
CreateContainer()
```
Creates an empty container for elements in the TDMorph node.

```python
ExposeTimers(x=0, y=0)
```
Creates a node that contains select CHOPS to the inner timers of each container.

```python
ExposeChannels(x=0, y=0)
```
Creates a node that contains par CHOPS to the inner parameter channles of each container.

```python
CreateFromLibrary(item, x=250, y=150, viewer=False)
```
Creates "item" object in the given coordinates. Enables the viewer if viewer=True. Possible items are:
  * PresetManager
  * PresetGrabber
  * PresetAnimator
  * ElementsContainer
  * MorphingTimers
  * MorphingChannels
  * Patterns
  * PresetComposer

```python
SelectObject(name, x=250, y=0)
```
A convenience method to create items from library with default locations. This is what TDMorph calls when a new item is invoked.

