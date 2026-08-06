# ParameterMorpher

**Part of the TDMorph Toolkit**  
Copyright © 2020–2026  
**Author:** [Darien Brito](https://www.darienbrito.com)  
**License:** **PROPRIETARY. Licensed, not sold.**  
**Version:** 4.9.0

> ParameterMorpher is a **commercial** component of the TDMorph toolkit, governed by the
> ParameterMorpher EULA (see the `LICENSE` operator inside the component). No
> redistribution, resale, sublicensing or sharing. No warranty.
>
> It is **not** MIT licensed and is not distributed from this repository. It is available
> through [Patreon](https://www.patreon.com/c/darienbrito). This page is reference
> documentation only.
>
> The MIT parts embedded inside it, the PresetManager engine and the `Lib/Patterns` library,
> keep their own MIT licence.

---

## 4.8.1

Three fixes, all found by mapping real hardware to the signal controls.

- **Deleting an element now stops its signal.** The element went but the signal kept running
  for the rest of the session, holding the transport clock on. With an LFO source it also
  logged an error every frame; with a pattern source it was silent, which is why it went
  unnoticed. Deleting a whole container was already handled in 4.8.0.
- **Mapping MIDI or OSC to a menu control now works.** Learning a knob onto the signal
  source, the sync mode, the interpolation curve or the random distribution looked like it
  worked and then did nothing: the control moved internally while the visible dropdown and
  the value it feeds stayed put. Sliders were never affected.
- **The signal enable checkbox can be mapped.** Its mapping marker sat on a part of the
  control that carries no value, so a mapping to it had nothing to write.

## 4.8.0

The signal and pattern controls are back inside each element, so several elements can show
their signals at once. They are now **built when you enable a signal and removed when you
disable it**, which is what keeps the size saving: an element with no signal costs the same as
it did in 4.7.x, and only the controls actually on screen exist.

- **Every element with a signal shows its own editor.** In expert mode each element carries a
  `sig` checkbox; ticking it opens that element's signal and pattern rows in place. Comparing
  two elements no longer means expanding one, reading it, then expanding the other.
- **Only what is visible is built.** The sync-step field follows the syncing mode (free running
  builds none at all), and the pattern editor is whichever of the two families your pattern
  type uses. Switching either swaps one control rather than rebuilding the row.
- **Disabling a signal frees the controls and keeps every value.** Your source, wave, pattern
  type, rate, range, smoothing and each pattern type's own values live on the element's
  parameters, not in the controls, so re-enabling restores exactly what you had.

**Sizes to plan a rig around.** An element without a signal is 218 operators. Enabling one adds
106 on the default free-running sequence pattern and at most 140 in the heaviest combination,
so twenty elements with every signal enabled land near 7,900 operators and nothing enabled
stays where it is today. Fifty all-enabled would be around 19,000, which is large enough to
slow the network editor: enable what you use.

**Fixed in the same release:** switching an element's signal source between LFO and Pattern
reset the saved choice for the source you switched to, so an LFO set to Square came back as
Sine. It now keeps both.

**Your existing projects carry forward.** No parameter or stored data changed.

## 4.7.1

Five fixes to the shared signals inspector introduced in 4.7.0.

- **The inspector cut off its own pattern editor.** It ignored the height the container gave it,
  so its controls rendered about three times too tall and the pattern section sat below the fold
  with no way to scroll to it. It also stopped short of the right edge instead of filling the
  width. Both are corrected, so the whole editor is visible.
- **Retargeting left the menus reading the previous element.** Expanding a second element moved
  the inspector, but the signal source, LFO and pattern menus still showed the first element's
  choices. They now follow the element being shown, including on the first retarget in a newly
  created container.
- **Deleting the element the inspector was showing** left it pointing at nothing, which raised
  errors across the panel until another element was expanded.
- **The two sequence fields did not commit what you typed.** A sequence entered in the inspector
  was displayed but never reached the element, so playback kept the previous values.
- **An element's interpolation curve and random distribution menus did not follow their
  parameter.** Changing either by script, by a MIDI or OSC mapping, or through a preset left the
  on-screen menu showing the old choice while the element morphed with the new one.

No parameters or stored data changed, so projects saved on 4.7.0 carry forward untouched.

## 4.7.0

The signal and pattern controls are no longer built into every element. They now live in one
inspector docked at the bottom of the container, and an element's expand toggle chooses which
element it edits. Every interpolatable element drops from 399 operators to 202, and the
component from 4455 to 4270, so a project with twenty elements saves roughly 3,900 operators.

**Your existing projects carry forward.** The parameters holding your signal and pattern setup
have not moved or changed, so nothing needs re-entering. The one difference in use is that two
elements' signals can no longer be shown at the same time, since there is a single inspector
rather than one per element.

The nine pattern scripting methods (`SetPseq` through `SetPbrown`) used to set values by
driving the on-screen widgets. They now write the element's stored pattern data directly, so
they keep working with the controls moved, and each pattern type is given the number of values
it actually takes.

## 4.6.1

- **The pattern editor follows the pattern type again.** Changing an element's pattern type
  stopped switching the editor below it, so picking a type like Pwhite still showed the
  sequence field belonging to the previous type, and any value edited in that state was saved
  into the previous type's slot. Playback was never affected: the signal always played the
  type you selected. Introduced in 4.6.0, where moving the signal engines into one shared
  service removed the part that told the editor which type was selected.
- **If you edited a pattern on 4.6.0**, check the values on each type, since an edit made
  after switching type may have landed on the wrong one.

---

## 4.6.0

- **Signals now run from one shared service instead of a copy inside every element.** A
  project with twenty elements used to run twenty signal engines; there is now a single
  service in the component that elements feed. Every element drops from 441 operators to
  399, and the component from 4574 to 4455.
- **Your existing projects carry forward.** The parameters holding your signal setup
  (source, LFO, pattern, frequency, sync mode, range, smoothing) have not moved or changed,
  the controls behave exactly as before, and nothing needs re-entering. With no signal
  running the service clock stays stopped, so idle cost is unchanged.

---

## 4.5.2

- **Test coverage only. Nothing in the component behaves differently** and your projects
  are unaffected. The bundled test suite now presses each button and checks what actually
  happened, rather than only checking that the method the button should call exists. That
  gap is what allowed the two dead buttons fixed in 4.4.4 to ship while every test passed.
  The suite grows from 150 checks to 190.

---

## 4.5.1

- **The header map icon is a crosshairs**, replacing the MIDI DIN plug it had inherited. One
  icon covers both protocols, so a MIDI connector was the wrong picture.
- **Fixes MIDI input being ignored.** The mapping service had stopped following the
  component's `MIDI` parameter, so a wired MIDI CHOP never reached it and nothing could be
  learned or routed. OSC was unaffected.

---

## 4.5.0: the MIDI/OSC mapping rebuild (breaking)

Version 4.5.0 replaces the MIDI/OSC mapping subsystem outright. **Mappings made in earlier
versions are not carried forward**, and eight parameters were retired, so any mappings you
already have need to be made again.

What changes for you:

- **One map mode, not two.** The separate MIDI and OSC controls are now a single **Map** icon in
  the header, shown whenever either a MIDI or an OSC input is wired on the Inputs page. Click it,
  click any control, then move a fader, knob or key to bind it. Both protocols share one list.
- **One mapping list.** The `Mappings` page is now **Manage Mappings** and **Clear Mappings**,
  replacing four pulses split across MIDI and OSC sections plus two location toggles. The editor
  shows every mapping in one table.
- **Per-mapping range.** Each mapping carries its own **Min** and **Max**, editable in the list.
  Previously all MIDI mappings shared one global input range.
- **Soft takeover.** Each mapping can be set to `pickup`, which waits until the incoming control
  reaches the parameter's current value before taking over, instead of jumping to wherever the
  fader happens to sit. `jump` is the default and matches the old behaviour.
- **Dead mappings are visible.** If a mapped control is renamed or removed, the row is marked
  `(missing)` in the list rather than silently doing nothing, and can be cleared with **Prune Dead
  Mappings**.
- **Retired parameters:** `Managemidimappings`, `Manageoscmappings`, `Clearmidimappings`,
  `Clearoscmappings`, `Togglelocationmidi`, `Togglelocationosc`, plus the two per-protocol section
  headers on the Mappings page.

Anything can now be a mapping target, not just the built-in controls: a mapping stores a control
and a parameter name, so any custom parameter can be driven.

The rebuild is also most of why the component dropped from 8853 to 4574 operators. The old system
gave every mappable widget its own learn overlay, so an interpolatable element cost 572 operators
in overlays alone; it is now one shared service plus a single marker operator per control.

---

## Overview

The ParameterMorpher is comprised of various components. To access full functionality you
need to interact with both the `extParameterMorpher` class and the `extElementsContainer`
class.

### What changed in 4.x

- **The embedded PresetManager engine is the shared multi-track engine.** ParameterMorpher
  embeds three copies of it, so per-track timing, end modes, curve shapes and preset schema
  v2 are all available here. See [PresetManager](PresetManager.md).
- **The mapping editor is an owned `listCOMP`**, replacing the previous palette TreeListers.
  ParameterMorpher carries no third-party content. As of 4.5.0 it is the shared ControlMapper
  editor described above.
- **The three embedded PresetManager paths editors are owned `ListView` instances.**
- Ships **empty**: no demo content, no stored presets, no bound paths, and **no container**.
  You create the first one yourself, which is the first step under
  [Getting started](#getting-started) below.

---

## Installation

1. Download `ParameterMorpher.tox` from [Patreon](https://www.patreon.com/c/darienbrito).
2. Drag the `.tox` into your TouchDesigner network, or use **File > Import > Component**.
3. Click the component's viewer to open the panel.

There is nothing else to install. The morphing engine is embedded, so ParameterMorpher does
not need a separate PresetManager (unlike [SceneLauncher](SceneLauncher.md), which attaches
an external one).

The licence terms are in the `LICENSE` operator inside the component. Keep the `.tox` in your
project folder or wherever you keep your components; it carries everything it needs.

## Getting started

The component opens **empty**, with no container and no elements. That is intentional: you
build the interface you want rather than deleting a demo first.

### 1. Create a container

Click **Create** in the header, the button whose tooltip reads *Create container*. A
`Container1` appears in the panel and the `Containers` parameter on the **Info** page goes
to 1.

The scripted equivalent, if you are building a project generatively:

```python
op('ParameterMorpher').CreateContainer()
```

Call it again for a second container. Use
`op('ParameterMorpher').ChangeOrientation(horizontal=True)` if you want them side by side
rather than stacked.

### 2. Add parameters

Drag parameters onto the container panel from the network:

- **Drag a single parameter** (from the parameter dialog) onto the container to get one
  slider bound to it. This works for any parameter, built in or custom.
- **Drag a whole node** onto the container to get one element per parameter, but note that
  this picks up **custom parameters only**. Dropping a node that has none, a Noise TOP for
  example, creates nothing. Drag that node's individual parameters instead.

Each element stays bound to its source parameter, so moving the slider drives the original
node directly.

### 3. Store a preset

<kbd>Shift</kbd> + <kbd>Left Click</kbd> an empty preset slot. The current value of every
element in that container is captured into it.

Set the parameters differently and store a second preset. Two presets is the minimum for
morphing to do anything visible.

### 4. Morph

<kbd>Left Click</kbd> a stored preset slot. The container morphs to it over its morph time,
using its interpolation curve.

Two variants are useful while you are still building:

- <kbd>Ctrl</kbd> + <kbd>Left Click</kbd> jumps straight to the preset with no interpolation.
- <kbd>Ctrl</kbd> + <kbd>Right Click</kbd> morphs in one second, for a quick transition check
  regardless of the configured time.

If you click a preset before adding any elements, the component tells you there is nothing to
apply it to. That is the expected message, not an error.

### 5. Where to go next

<kbd>Right Click</kbd> empty space inside a container for its context menu: *Reset
parameters*, *Clear parameters*, *Rename presets in order* and *Add script*.

The header dropdown builds the companion tools against your containers: *Timers*, *Channels*,
*Grabber*, *Animator* and *Patterns*.

Full key and mouse reference: [SHORTCUTS.md](../SHORTCUTS.md). Everything below this point is
the Python API.

---

## Signals and patterns

Any interpolatable element can drive its parameter continuously, independently of preset
morphing. A signal is either an **LFO** (a periodic wave) or a **pattern** (a stepped sequence
of values). It is chosen per element and runs on the component's own clock.

### Where the controls live

Each element carries its own controls, and they are built on demand. In expert mode an
element shows a `sig` checkbox; enabling it builds that element's signal and pattern rows,
disabling it removes them again. Several elements can therefore show their signals at once.

Only the controls that are visible exist: the sync-step field matches the syncing mode (free
running has none), and the pattern editor is the family your pattern type uses. Changing
either swaps that one control.

The controls are a view, not the engine. Every element runs its signal whether or not its
controls are built, and every value you set lives on the element's parameters below, which is
why disabling and re-enabling restores exactly what you had.

### The model

Signal state lives on the element's `MorphSettings` operator as fifteen custom parameters, and
the engine reads only those. Setting them from Python does exactly what the pane does.

| Parameter | Meaning |
|---|---|
| `Enablesignal` | Turns the element's signal on. Nothing runs while this is off. |
| `Signalsource` | Selects `LFO` or `Pattern`. |
| `Lfo` | Wave shape, used when the source is `LFO`. |
| `Pattern` | Pattern type, used when the source is `Pattern`. |
| `Frequency` | Rate in Hz, used when the syncing mode is free running. |
| `Syncingmode` | Free running, or locked to beats, bars or sixteenths. |
| `Manualtrigger` | Advances a pattern by one step. |
| `Beatfactor`, `Barfactor`, `Sixteenthsfactor` | Multipliers for the locked syncing modes. |
| `Rangex`, `Rangey` | Output range. The raw signal is remapped into it. |
| `Smoothingactive` | Turns output smoothing on. |
| `Smoothrange`, `Smoothlength` | Smoothing amount and window length. |

Pattern values are stored separately, as JSON on the element's `Patterndata` parameter. Each
pattern type keeps its own entry, so switching type and switching back preserves what you
entered. Projects made before 4.7.0 migrate automatically the first time they load.

### Pattern types

Nine methods on an element select a pattern type and set its values in one call. They are the
supported way to script patterns; writing `Patterndata` by hand is not.

| Method | Produces |
|---|---|
| `SetPseq(sequence)` | The sequence in order, looping. |
| `SetPrand(sequence)` | Random picks from the sequence. |
| `SetPxrand(sequence)` | Random picks with no immediate repeats. |
| `SetPshuffle(sequence)` | The sequence shuffled once, then looping. |
| `SetPwrand(sequence, weights)` | Random picks biased by `weights`. |
| `SetPseries(start, step, length)` | An arithmetic series. |
| `SetPgeom(start, grow, length)` | A geometric series. |
| `SetPwhite(lo, hi)` | Uniform random values between `lo` and `hi`. |
| `SetPbrown(lo, hi, step)` | Brownian motion bounded by `lo` and `hi`. |

`SetPseries` and `SetPgeom` are finite by definition, so the engine wraps them to repeat
rather than letting the signal run dry and freeze.

### Under the hood

One `SignalEngine` service at the component root drives every element, rather than each
element carrying its own engine. Only active signals occupy the service's table, and its clock
runs only while that table has a row, so a component with no signals enabled costs nothing
when idle.

The service API is documented in [Help/SignalEngine.md](../Help/SignalEngine.md). To resync
every LFO in a container to a common phase, call `HardSyncLFOs()` on the container.

---

## exParameterMorpher

The `extParameterMorpher` class is part of the **TDMorph** system for **TouchDesigner**.  
It manages **container creation**, **library tool instantiation**, and **parameter exposure** within the TDMorph module.  

This class serves as a **high-level manager** for creating interface elements, preset-related tools, and morphing utilities from the internal library.  
It adheres to a **Model–View–Controller (MVC)** structure, functioning as the *Model*—that is, the logic and data layer independent of UI interactions.

---

## Table of Contents

- [Architecture](#architecture)
- [Initialization](#initialization)
- [Public Methods](#public-methods)
  - [Container Management](#container-management)
  - [Preset Manager Integration](#preset-manager-integration)
  - [UI Layout Control](#ui-layout-control)
  - [Reporting](#reporting)
- [Design Philosophy](#design-philosophy)

---

## Architecture

| **Attribute** | **Description** |
|----------------|-----------------|
| **Class** | `extParameterMorpher` |
| **Role** | Manages creation of containers, preset-related tools, and exposure of morphing data. |
| **Type** | Model / Logic Controller |
| **Design Pattern** | Part of the TDMorph MVC architecture. |
| **Usage Context** | Used internally to instantiate morphing-related utilities and connect Preset Managers to UI containers. |

---

## Initialization

```python
morpher = op('ParameterMorpher')
```
## Public Methods

### Container Management

- **`GetContainer(n)`**  
  Retrieves a specific container UI by index.  

- **`CreateContainer()`**  
  Creates a new container for slider-based UI elements and links it to the `Elements` component.  

---

### Preset Manager Integration

- **`ExposeTimers(x=0, y=0)`**  
  Creates a composite component exposing **Preset Manager timer channels**.  


- **`ExposeChannels(x=0, y=0)`**  
  Creates a component exposing all **parameter channels** of the UI sliders.  

---

### UI Layout Control

- **`ChangeOrientation(horizontal=False)`**  
  Changes the alignment of UI containers between horizontal and vertical layouts.  

### Reporting

- **`ReportResult(msg, title)`**  
  Displays a popup dialog in TouchDesigner and logs a formatted message to the console.  

---

## Design Philosophy

- **UI Independence:** Logic operates independently of any UI behavior.  
- **Modularity:** Provides an interface layer for morphing and preset operations without visual dependencies.  
- **Automation-Friendly:** Allows automatic generation of morphing tools and managers in project setups.  
- **Extensibility:** Encourages addition of new library components without structural changes.  
- **MVC Integrity:** Respects the TDMorph Model–View–Controller separation of concerns.

---

## extElementsContainer

---

## Overview

The `extElementsContainer` class manages **groups of UI elements** (sliders, toggles, menus, etc.) in **TDMorph**, providing a high-level interface between the user interface and the internal `PresetManager`.  

It acts as a **UI-focused controller**, handling element creation, parameter binding, preset management, and synchronization between visual and logical layers.  

This class is primarily used to create and manage **parameter-linked sliders** for morphing and randomization within **TouchDesigner**.

---

## Table of Contents

- [Architecture](#architecture-1)
- [Stored Properties](#stored-properties)
- [Container and UI Management](#container-and-ui-management)
- [Preset Management](#preset-management)
- [Randomization and Morphing](#randomization-and-morphing)
- [Sequence Control](#sequence-control)
- [Utility and Miscellaneous](#utility-and-miscellaneous)
- [Callbacks](#callbacks)
- [Design Philosophy](#design-philosophy-1)
- [Dependencies](#dependencies)

---

## Architecture

| **Attribute** | **Description** |
|----------------|-----------------|
| **Class** | `extElementsContainer` |
| **Role** | Manages groups of morphing UI elements for parameter control. |
| **Type** | UI Controller / Manager |
| **Design Pattern** | Part of the TDMorph MVC architecture. |
| **Usage Context** | Used to create UI bindings, manage presets, randomization, and morph transitions. |

---

## Stored Properties

| **Property** | **Type** | **Description** |
|---------------|----------|-----------------|
| `BindedPaths` | `dict` | Dictionary mapping cross-check names to binding data for parameters. |
| `containerName` | `str` | Name of the container instance. |
| `NumberOfElements` | `int` | Number of elements contained in the UI container. |
| `GlobalStatus` | `bool` | Whether global morphing and randomization are enabled. |

---

### Container and UI Management

- **`Name`** *(property)*  
  Gets or sets the container’s name.  

- **`Delete()`**  
  Deletes all UI elements and destroys the container panel.  

- **`UpdateSize(sizeLimit=720)`**  
  Adjusts the height of the container based on its content.  

- **`HardSyncLFOs()`**  
  Resynchronizes all internal LFOs across contained elements.  

- **`ChangePresetsNum(newVal)`**  
  Changes the number of presets available in the container.  

- **`GetBindedKeys()`**  
  Returns a list of all keys from the `BindedPaths` dictionary.  

- **`GetPresetManager()`**  
  Returns the internal `PresetManager` component reference.  

- **`GetElementsValues()`**  
  Returns a dictionary of element values and ranges.  

- **`CreateElement(source, parameter, dataSource='parameter', customName=None)`**  
  Creates and binds a new UI element linked to a parameter or preset.  
  Handles the correct UI type allocation, binding, and reference registration.  

- **`AddScript()`**  
  Creates a special script element that executes custom code when triggered.  

- **`ClearParameters()`**  
  Removes all UI parameters after confirmation.  

- **`ResetParameters()`**  
  Resets all UI elements to their default stored values.  

- **`RenamePresetsOrder()`**  
  Renames and reorders presets based on current UI order.  

- **`ExpertMode(value)`**  
  Enables or disables “Expert Mode” for advanced control settings.  

---

### Preset Management

- **`ExportPresetsJSON()`**  
  Exports all presets, bindings, and element data to a `.json` file.  
  Used for saving full configuration states including UI bindings.  

- **`ExportPresetManager()`**  
  Creates a copy of the internal `PresetManager` for standalone use.  

- **`ImportPresetsJSON()`**  
  Imports presets and bindings from a `.json` file, reconstructing the UI and restoring order.  

- **`ClearPresets(overwriteWarning=True)`**  
  Clears all presets in both macro and micro (local) managers.  

---

### Randomization and Morphing

- **`SyncClocks()`**  
  Synchronizes morph timers across all linked elements.  

- **`SetRandom(mode=None)`**  
  Randomizes parameter values globally or per element.  

- **`MorphRandom(mode=None)`**  
  Performs a morph transition toward randomized target values.  

---

### Sequence Control

- **`PresetsSequence(sortKeys=False, keysSequence=None)`**  
  Traverses presets sequentially across all linked elements.  

---

### Utility and Miscellaneous

- **`Interpolation`** *(property)*  
  Gets or sets the interpolation curve used for morphing.  

- **`Distribution`** *(property)*  
  Gets or sets the random distribution type.  

- **`GlobalTime`** *(property)*  
  Toggles global vs local morph timing control.  

- **`Automorph` / `Automorphs`** *(property)*  
  Controls automatic morph playback and its count.  

- **`Time`** *(property)*  
  Gets or sets the morphing duration.  

- **`NumberOfPresets`** *(property)*  
  Gets or sets the total number of available presets.  

- **`StorePreset(slot)`**  
  Stores the current preset into a numbered slot.  

- **`SetPreset(slot)`**  
  Loads and activates a stored preset.  

- **`DeletePreset(slot)`**  
  Deletes a stored preset by index.  

- **`GetElement(elementNum)`**  
  Returns a specific UI element by its numeric order.  

- **`Freeze(value)`**  
  Locks or unlocks the entire UI, preventing accidental changes.  

---

## Callbacks

The following methods execute when connected callback scripts are defined:

- **`OnMorphingStart(manager, morphingType, presetName)`**  
  Triggered when a morphing process starts.

- **`OnMorphingEnd(manager, morphingType, presetName)`**  
  Triggered when a morphing process ends.

- **`OnPresetCall(manager, morphingType, presetName)`**  
  Triggered when a preset is invoked manually or programmatically.

All callback functions look for an external module defined in  
`Elementscontainercallbacks` and call corresponding `onMorphingStart`,  
`onMorphingEnd`, or `onPresetCall` functions.

---

## Design Philosophy

- **UI-Driven Logic:** Designed for dynamic UI creation and interaction with parameters.  
- **Modularity:** Each container acts independently but can synchronize with others.  
- **Non-Destructive:** Parameters can be freely created, rebound, or deleted. 
- **Automation-Friendly:** Supports scripting, callback hooks, and sequenced morphing.  
- **MVC Compliance:** Acts as a **Controller** in the TDMorph architecture, linking UI (View) and PresetManager (Model).

---

## Dependencies

### TouchDesigner Components
- `PresetManager`
- `PresetMorpher`
- `Menus`
- `Elements`
- `Parameters`
- `TDResources`
- `Lib/Elements/*`

### Python Libraries
- `TDStoreTools.StorageManager`
- `json`

---
