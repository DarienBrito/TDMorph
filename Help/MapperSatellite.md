# Mapper Satellite

The per-element side of the mapping system. Found inside both the MIDI and OSC containers,
these operate as satellites for the main [Mapper](Mapper.md) class.

Implemented by `extMapper`, present in both ParameterMorpher and SceneLauncher.

> **PROPRIETARY. Licensed, not sold.** Part of the commercial ParameterMorpher and
> SceneLauncher components, available through
> [Patreon](https://www.patreon.com/c/darienbrito), not from this repository.

This file was previously named `MapperSatelllite.md`, with three `l`s.

## Core level methods

### Promoted

```python
SetActiveListener(state=True)
```
Sets auto-learning on or off.

```python
UnMap()
```
Remove this element from the mappings list.

## Interaction

With MIDI or OSC enabled, on a mappable control:

| Action | Result |
|---|---|
| <kbd>left click</kbd> | Activate auto-learning. Expects a MIDI or OSC change to map to. |
| <kbd>right click</kbd> | Set the parameter to the learned MIDI or OSC signal. |
| <kbd>middle click</kbd> | Delete the mapping. |

The mapping inspectors are an owned `listCOMP` editor. Both sold tools carry no third-party
lister content.
