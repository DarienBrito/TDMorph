# Preset Buttons

## Core-level methods

### Promoted

```python
GetPresetsSequence()
```
Gets the order on which the presets are visually arranged.

```python
Reorder(name, source, receiver)
```
Re-ordering is a bit tricky, but I do so by mantaining the buttons order and simply altering the preset name they refer to. "source" is origin "receiver" is target.

```python
Spawn(val)
```
Create as many presets as defined by val

### Private

```python
create(n)
```
Creates n presets.

```python
destroy(n)
```
Deletes n presets.

```python
getLast()
```
Gets last preset in the stack.

```python
getNum()
```
Get total number of available presets.
