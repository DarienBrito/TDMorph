# TDMorph 

## Core Methods

### Public

```python
CreateContainer()
```
Creates an empty container for elements in the TDMorph node.

```python
CreateFromLibrary(item, x=250, y=150, viewer=False)
```
Creates "item" object in the given coordinates. Enables the viewer if viewer=True. Possible items are:
  * 'PresetManager'
  * 'PresetGrabber'
  * 'PresetAnimator'
  * 'ElementsContainer'
  * 'MorphingTimers'
  * 'MorphingChannels'
  * 'Patterns'
  * 'SceneLauncher'

```python
ExposeChannels(x=0, y=0)
```
Creates a node that contains par CHOPS to the inner parameter channles of each container.

```python
ExposeTimers(x=0, y=0)
```
Creates a node that contains select CHOPS to the inner timers of each container.

```python
GetContainer(n)
```
Get the container at n position.

```python
ReportResult(msg, title)
```
Launches a TDMorph-formatted pop up window with the given message and title.

```python
SelectObject(name, x=250, y=0)
```
A convenience method to create items from library with default locations. This is what TDMorph calls when a new item is invoked.

### Private

```python
containersExist()
```
True if there are containers, false if not.

```python
createBase(name, x=-200, y=150, color=(0.1, 0.8, 0.1))
```
Creates a base on the parent() level with given properties.

## UI Methods

### Public

```python
ChangeOrientation(horizontal=False)
```
Changes the look of TDMorph from vertical to horizontal. Only useful if there is more than a single container in the Window.

