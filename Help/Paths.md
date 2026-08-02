# Paths

The database of operators the PresetManager tracks, and their per-path settings. Lives at
`PresetManager/Paths`.

Nodes are marked with the manager's `Trackingtag` value (`TDMorphPath` by default), which is
how a node that has been moved is found again.

Version 4.1.2. Capitalized methods are promoted and are the supported API.

Full reference: [Documentation/PresetManager.md](../Documentation/PresetManager.md#tracked-paths).

## Core level methods

### Properties

```python
TrackingTag = str
```
Get/set the tag written onto tracked nodes.

### Promoted

```python
AutoUpdatePaths()
```
Reconcile nodes that have moved by scanning for the tracking tag. Returns the path changes applied, which the PresetManager feeds to UpdatePaths to re-key the presets.

```python
Clear(storedSettings=True, overwriteWarning=True)
```
Remove all entries, cleaning up every tracked node's TDMorph data. Prompts for confirmation unless overwriteWarning is False.

```python
Create(path, addTrackingTag=True, settings=None)
```
Register a path: tag the node, store its tracking path and record its settings.

```python
Delete(path, storedSettings=True, ignoreWarning=False)
```
Remove a path from the database and strip its TDMorph tag and storage.

```python
GetItem(path, item)
```
Read one setting for a stored path, for example its time or curve.

```python
GetNumPaths()
```
How many paths are tracked.

```python
GetPathsKeys()
```
Every tracked path.

```python
Inject(path, data)
```
Insert or overwrite a raw settings block for a path.

```python
IsStoredPath(v)
```
Whether the given path is tracked.

```python
NewDrop(source, name=None)
```
Create a new entry from a drag-and-drop of an operator onto the editor.

```python
OpenUI()
```
Open the paths editor.

```python
OverwriteAllItems(item, val)
```
Set one item to a value on every stored path.

```python
OverwriteItem(path, item, val)
```
Set one item on a single stored path.

```python
Replace(oldPath, newPath)
```
Move an entry's contents from one path to another.

```python
ReportResult(msg, title)
```
Launches a TDMorph-formatted pop up window with the given message and title.

```python
StandardPopDialog(text, title, buttons, callback, details=None, textEntry=None)
StandardPopMenu(info, items, callback)
```
Open a standard pop-up dialog or menu wired to a callback. Guarded on TouchDesigner's own `op.TDResources`.

```python
Update()
```
Rebuild the UI reference table from the stored paths.

### Private

```python
getChangedPaths()
```
Scan the search scope for tracked nodes that have moved.

## The editor

The paths editor is an owned MIT [ListView](ListView.md) instance, not a palette Lister.

| Action | Result |
|---|---|
| Drag an operator onto the editor | Register it as a tracked path. |
| Double-click a row | Open that node in the View pane. |
| Click the View column | Open or reuse one floating network pane focused on the node. |
| Right-click a column header | Rename or realign the column. |
| Right-click empty space | The general Update and Clear menu. |

The per-path `Time`, `Curve`, `a`, `b` and `n` columns appear only when the manager's
**Multi-Track Engine** toggle is on.
