# ControlMapper

The MIDI/OSC mapping service. One instance sits inside ParameterMorpher and SceneLauncher and
serves both protocols from a single list of mappings.

Class: `extControlMapper`. Version 0.1.2.

> **MIT licensed**, but distributed only inside the commercial ParameterMorpher and
> SceneLauncher components, which are available through
> [Patreon](https://www.patreon.com/c/darienbrito), not from this repository.

Introduced in ParameterMorpher 5.0.0 and SceneLauncher 5.0.0, replacing the per-widget MIDI and
OSC learn overlays and the separate `Mapper` and `MapperSatellite` classes. Mappings made before
those versions are not carried forward.

A mapping stores a channel, a target operator, a parameter name, an input range, and a takeover
mode. Because the target is a control plus a parameter name rather than a fixed widget, any custom
parameter can be driven, not just the built-in controls.

## Properties

```python
Mappings
```
Every mapping as a dict, in table order.

```python
NumMappings
```
How many mappings are currently stored.

```python
MapMode
```
True while map mode is on.

## Map mode and learning

```python
SetMapMode(state)
```
Enter or leave map mode. Reveals every registered target and cancels any pending arm.

```python
Arm(widget, parName='Value')
```
Arm `widget.par[parName]` so the next incoming channel binds to it.

```python
OnTargetClick(target)
```
Handle a click on a `MapTarget`. Arms its widget, or disarms it if it was already armed.

```python
Map(chan)
```
Bind the armed target to `chan`. Consumes the arm. Returns True when a row was written.

```python
Unmap(chan, target, parName='')
```
Remove mappings matching channel and target, and parameter name when given. Returns how many rows
were removed. All three arguments are strings, not operators.

```python
Cancel()
```
Disarm without changing the map.

```python
IsArmed()
```
True while something is armed.

```python
ArmedTarget()
```
The widget currently armed for learning, or None.

```python
ArmRow(rowIndex)
```
Arm an existing mapping for re-learn, so the next channel re-keys that row.

```python
ArmedRowIndex()
```
The 1-based table row currently armed, or -1.

## Routing

```python
Route(chan, val)
```
Send one normalized channel value, in the range 0 to 1, to every target bound to it. Returns how
many targets were written.

```python
Recompile()
```
Force a rebuild of the routing dictionary. The editor calls this after a table edit.

## Editing mappings

```python
SetMappingRange(rowIndex, lo, hi)
```
Set one mapping's target range, by 1-based table row. A learned menu parameter spans 0 to N, not
0 to N-1, because TouchDesigner floors a menu value to an index.

```python
SetMappingTakeover(rowIndex, mode)
```
Set takeover to `'jump'`, which writes immediately, or `'pickup'`, which waits until the incoming
control crosses the parameter's current value before taking over.

```python
ToggleMappingTakeover(rowIndex)
```
Flip one mapping between `jump` and `pickup`. Returns the new value, or an empty string on failure.

```python
SetMappingChannel(rowIndex, chan)
```
Re-key one mapping onto a different channel.

```python
DeleteMappingRow(rowIndex)
```
Delete one mapping by table row.

```python
ReorderMappings(order)
```
Rewrite the table in the given order, as 0-based data indices. This is what backs drag-reorder in
the editor.

## Dead mappings

```python
DeadRows()
```
The 1-based indices of mappings whose target or parameter no longer resolves. Dead mappings are
kept and reported rather than silently skipped, so a renamed control shows as `(missing)` instead
of quietly doing nothing.

```python
PruneDead()
```
Delete every dead mapping. Returns how many went.

## Clearing

```python
ClearMappings()
```
Drop every mapping. This is the model call and does not ask first.

```python
ConfirmClearMappings()
```
Ask before dropping every mapping. Returns True when the map was cleared outright, False when a
confirmation is pending. This is what the Clear pulse and the editor's "Clear all" both route
through.

## Registration

```python
RegisterTargets(targets)
```
Declare which `MapTarget` operators exist. Hosts that build controls at runtime call this on
create and destroy. Returns how many were registered.

```python
ScanTargets()
```
Find targets by tag under `Maproot` and register them. Type filtered on purpose, since an
unfiltered search on a large host is expensive.

## UI level methods

```python
OpenEditor()
```
Open the mapping editor.

```python
OnBlink(val)
```
Blink driver for the armed target. One execute operator serves the whole host.
