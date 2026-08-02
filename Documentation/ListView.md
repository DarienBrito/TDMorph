# ListView

**Part of the TDMorph Toolkit**  
Copyright © 2026  
**Author:** [Darien Brito](https://www.darienbrito.com)  
**License:** [MIT License](https://opensource.org/license/mit)  
**Version:** 1.0.3

---

## Overview

`ListView` is a reusable **flat-columnar list widget** built on TouchDesigner's built-in `listCOMP`. It gives you a data grid with a declarative column spec, inline editing, drag-to-resize columns, drag-to-reorder rows and a pluggable behaviour module, without any palette or third-party content.

It is both a **standalone component** you can drop into your own projects and the widget the rest of TDMorph is built on: the PresetManager paths editor and the SceneLauncher scene and preset lists are all ListView instances.

Because it is MIT licensed, you are free to use it in commercial and closed-source work.

---

## Table of Contents

- [Architecture](#architecture)
- [Quick start](#quick-start)
- [Custom parameters](#custom-parameters)
- [Columns](#columns)
- [Rows](#rows)
- [The Callbacks contract](#the-callbacks-contract)
- [Public methods](#public-methods)
- [Theming](#theming)
- [Interaction reference](#interaction-reference)
- [Reuse recipe](#reuse-recipe)
- [Testing](#testing)

---

## Architecture

| **Attribute** | **Description** |
|---|---|
| **Class** | `extListView` |
| **Role** | Generic flat-columnar list rendering and interaction. |
| **Built on** | The native `listCOMP`. No palette Lister, no `colDefine` or `listerConfig`. |
| **License** | MIT |

The component separates three concerns:

- **What data** comes from the `Host` parameter.
- **How it behaves** comes from the `Callbacks` parameter, a DAT whose module defines the hooks.
- **How it looks** comes from the theme module plus the Colors and Look parameter pages.

### Child operators (the names are the contract)

| **Operator** | **Type** | **Role** |
|---|---|---|
| `list` | listCOMP | The grid itself. `list_callbacks` routes events to `extListView`. |
| `rows` | tableDAT | Data mirror, for debugging and inspection. |
| `listViewTheme` | DAT | The theme module. Point it at any module matching the theme schema. |
| `rclickExec` | panelexecuteDAT | Watches `list.rselect` and dispatches right-clicks. |
| `extListView` | textDAT | The engine class. Shared: do not edit per copy. |

---

## Quick start

Host-less use, pushing data straight in from Python:

```python
lv = op('ListView')

lv.SetColumns([
    {'key': 'n',     'kind': 'index', 'width': 40, 'label': '#'},
    {'key': 'name',  'label': 'Name',  'width': 160, 'editable': True},
    {'key': 'level', 'label': 'Level', 'kind': 'value', 'editable': True, 'align': 'right'},
    {'key': 'del',   'label': '',      'kind': 'icon', 'action': 'delete', 'width': 30},
])

lv.SetRows([
    {'name': 'intro',  'level': 0.4},
    {'name': 'chorus', 'level': 1.0},
])
```

That renders a working, editable, reorderable grid. To react to edits and clicks, add a `Callbacks` DAT (see below).

---

## Custom parameters

### ListView page

| **Parameter** | **Type** | **Default** | **Description** |
|---|---|---|---|
| `Host` | COMP | `''` | The component owning the data model. Callbacks reach it via `lister.par.Host.eval()`. |
| `Callbacks` | DAT | `''` | The behaviour module for this instance. Resolves relative to the lister's parent, so a sibling name works. |
| `Editable` | Toggle | `On` | Master switch for inline editing. A column must also set `editable`. |
| `Header` | Toggle | `On` | Show the column header row. |
| `Emptyheader` | Toggle | `Off` | Keep the header visible when there is no data yet, instead of rendering fully empty. |

### Look page

| **Parameter** | **Type** | **Default** | **Description** |
|---|---|---|---|
| `Headerfontsize` | Int | `11` | Header text size. |
| `Cellfontsize` | Int | `11` | Cell text size. |
| `Cellpadding` | Int | `10` | Horizontal padding inside a cell. |
| `Rowseparators` | Toggle | `On` | Draw a line between rows. |
| `Separators` | Toggle | `Off` | Draw a line between columns. |

### Colors page

Eight RGBA parameters override the theme without editing code: `Rowcolor` and `Rowcoloralt` (a zebra pair, match them to flatten), `Headercolor`, `Headertextcolor`, `Textcolor`, `Valuecolor`, `Selectcolor`, `Hovercolor` and `Dividercolor`.

### About page

`Author`, `Version` and the `Readme`, `Help`, `Support` and `Website` pulse buttons.

---

## Columns

One dict per column, returned from `ListViewColumns(lister)` or pushed with `SetColumns(spec)`.

```python
{key, label, width, stretch, align, kind, editable, action, raction,
 glyph, color, iconfont, iconsize, help}
```

| **Field** | **Values** | **Description** |
|---|---|---|
| `key` | str | Required. The key this column reads from each row dict. |
| `label` | str | Header text. |
| `width` | int | Column width in pixels. |
| `stretch` | bool | Let the column absorb leftover width. |
| `align` | `left` \| `center` \| `right` | Text alignment. Default `left`. |
| `kind` | `text` \| `value` \| `icon` \| `badge` \| `swatch` \| `index` | Cell renderer. Default `text`. |
| `editable` | bool | Allow inline editing (needs the master `Editable` on too). |
| `action` | str | A left-click fires `ListViewAction(lister, action, row)`. |
| `raction` | str | The same for a right-click. |
| `glyph` | str | Icon character for `icon` columns. |
| `color` | tuple | Accent colour for icons, badges and swatches. |
| `help` | str | Per-column tooltip. |

### Column kinds

- **`text`** plain string.
- **`value`** JSON-typed. Numbers, strings, booleans and null get their own colour, and an inline edit is coerced back to the old value's type.
- **`index`** an automatic 1-based row number that reads the rendered position, so it renumbers itself for free after a reorder. Needs no key in the row data.
- **`icon`** a glyph button. Pair it with `action` or `raction`.
- **`badge`** a small filled label.
- **`swatch`** a colour chip, from an RGB value in the row.

The spec is copied at build time. Per-key width, alignment and label overrides are stored on the component, so a user's drag-resize, rename or realign survives a refresh, a reload and a save.

---

## Rows

A list of dicts keyed by the column keys:

```python
[{'name': 'intro', 'level': 0.4}, {'name': 'chorus', 'level': 1.0}]
```

Carry a private id (for example `_key`) when you need stable host-side identity across reorders. The selected row index is stored on the component.

---

## The Callbacks contract

Point the `Callbacks` parameter at a DAT whose module defines any of these module-level functions. All are optional. Each takes the ListView component as its first argument, so one module can drive several lists, or you can write one module per list.

```python
ListViewColumns(lister)                  # -> column spec list
ListViewRows(lister)                     # -> list of row dicts
ListViewAction(lister, name, row)        # action / raction click
ListViewActivate(lister, row)            # double-click a row
ListViewEdit(lister, row, key, new, old) # committed inline edit
ListViewReorder(lister, order)           # new order, as data indices
ListViewContext(lister)                  # right-click on empty space
ListViewHeaderMenu(lister, col)          # right-click a header (overrides the built-in menu)
ListViewSelect(lister, row)              # row pressed
ListViewDrop(lister, source)             # a panel drop landed
```

Dispatch order is **Callbacks DAT module, then the `Host` component's promoted method, then a lean built-in default**. So an instance with no `Callbacks` falls back to its `Host`, and with neither, the hooks simply do nothing.

The column header rename and align menu is **built in**. You only need `ListViewHeaderMenu` if you want to replace it.

Keep the Callbacks DAT outside the widget itself, as a sibling or a child of the host.

### A minimal Callbacks module

```python
def ListViewColumns(lister):
	return [
		{'key': 'name', 'label': 'Name', 'width': 160, 'editable': True},
		{'key': 'del',  'label': '', 'kind': 'icon', 'action': 'delete', 'width': 30},
	]

def ListViewRows(lister):
	host = lister.par.Host.eval()
	return [{'name': n} for n in host.MyNames()]

def ListViewEdit(lister, row, key, new, old):
	lister.par.Host.eval().Rename(old, new)

def ListViewAction(lister, name, row):
	if name == 'delete':
		lister.par.Host.eval().Delete(row)
		lister.Refresh()
```

---

## Public methods

```python
Build()
```
Re-read the column spec from the host, then refresh the rows.

```python
Refresh()
```
Re-read the row data from the host and re-render.

```python
SetColumns(spec)
SetRows(rows)
```
Push a column spec or row data directly, for host-less or programmatic use.

```python
Rows()
SelectedRow()
```
The current row data, and the selected row index (`-1` when nothing is selected).

```python
SetActiveRow(dataIndex)
```
Select and highlight a row by its 0-based data index, and re-render. Pass `-1` to clear.

```python
SetColumnAlign(col, align)
SetColumnLabel(col, label)
```
Set a column's alignment or header label and persist it, the same way the built-in header menu does.

```python
Reorder(order)
```
Apply a new row order and notify the host.

```python
ReorderDict(d, order)
```
A static helper that reorders an ordered dependable dict in place, for use inside `ListViewReorder`.

---

## Theming

`listViewTheme` is any module exposing the theme schema: fonts, `ROW_A` and `ROW_B`, `HEADER_BG` and `HEADER_FG`, `SELECT_BG` with `SELECT_ALPHA`, `TEXT`, `TEXT_DIM`, `ACCENT`, `BADGE_TEXT`, `OTHER_COLOR`, `VALUE_COLORS`, `TYPE_COLORS`, `PAD_X`, `DBLCLICK_SECONDS` and the glyph set. Colours are RGB 3-tuples; the engine appends alpha.

Theming is **fail-soft**: a missing render symbol falls back to a neutral default, so a partial theme still renders. A misspelled symbol still raises, so typos are not silently swallowed.

`HOVER_BG`, `HEADER_DIVIDER` and `ROW_DIVIDER` are feature-gated. Leave one out and that hover or separator is simply off.

Fonts must be an **installed OS family**; a `.ttf` path is ignored by `listCOMP`. Verdana, Courier New and Material Design Icons ship with both macOS and Windows, which is why the default theme uses them.

For per-instance tweaks, prefer the Colors and Look parameter pages over editing the theme module.

---

## Interaction reference

| **Action** | **Result** |
|---|---|
| Double-click an editable cell | Inline edit. The value is coerced back to the old type on commit. |
| Drag a column border | Resize that column. The width persists. |
| Right-click a column header | Rename or realign the column. |
| Drag a row up or down | Reorder. Fires `ListViewReorder`. |
| Double-click a row | Fires `ListViewActivate`. |
| Left or right click an action column | Fires `ListViewAction`. |
| Right-click empty space | Fires `ListViewContext`. |
| Drop a dragged operator onto the list | Fires `ListViewDrop` with the dragged path. |

---

## Reuse recipe

1. Drop `ListView.tox` into your project, or clone the component if you want several lists sharing one engine. Custom parameter values do not clone-sync, so each clone keeps its own look and its own `Host` and `Callbacks`.
2. Set **`Host`** to the component that owns your data.
3. Write the behaviour DAT implementing the hooks you need, place it outside the widget, and set **`Callbacks`** to it by name.
4. Point **`listViewTheme`** at your theme module, then tune the Colors and Look pages.

A new column `kind` means adding a renderer branch to the shared engine, which touches every copy. A new interaction is just a new hook in your own Callbacks DAT, which touches only that instance.

---

## Testing

```python
op('ListView/Tests/tests').module.RunAndReport()
```

127 checks ship in 1.0.3, covering rendering, the column spec, edit coercion, reorder, the double-click detector and row identity.
