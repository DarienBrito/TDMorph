# TDMorph 4.1.2 beta

This branch carries a **beta** of the free, MIT-licensed part of TDMorph. It is here to be
tested on real projects before it becomes the stable release.

If you need something dependable for a show next week, stay on
[3.2.1](https://github.com/DarienBrito/TDMorph/releases/tag/v3.2.1).

---

## What is in it

| Component | Version | What it is |
|---|---|---|
| **PresetManager** | 4.1.2 | Preset storage plus the multi-track morphing engine. The core of TDMorph. |
| **PresetInspector** | 1.5.4 | Preset JSON viewer and value editor. Attaches to a PresetManager. |
| **JSONTree** | 1.5.4 | Reusable collapsible JSON tree viewer with inline editing. |
| **ListView** | 1.0.3 | Reusable flat-columnar list widget built on the native `listCOMP`. |

PresetInspector, JSONTree and ListView have never been released here before. PresetManager
jumps from 3.2.1 to 4.1.2.

ParameterMorpher and SceneLauncher are **not** part of this release. They remain available
through [Patreon](https://www.patreon.com/c/darienbrito).

---

## Installing

Drag the `.tox` you want into your project, or use **Component > Import Component**.

Each component is self-contained: no external files, no palette dependencies and no
third-party content. PresetInspector expects a PresetManager to attach to, and defaults to
the sibling name `PresetManager`, so if you drop the two side by side it works with no
configuration.

Nothing is installed globally and nothing is written outside your project.

---

## What most needs testing

### Upgrading an existing 3.2 project

This is the single most valuable thing you can try.

Preset schema v2 moved the timing fields from the top of a preset into each tracked path.
Presets written by 3.2 are **migrated automatically** when they are loaded, and migration is
idempotent, so nothing breaks if it runs twice. It has been tested here, but not against
the variety of real projects you have.

**Please back up your project and export your presets to JSON before opening them with
4.1.2.** If a migration goes wrong, that export is what lets you recover, and it is what
makes the bug report actionable.

Worth checking specifically:

- Your presets still recall the values you stored.
- Curves still reach their target at the right point in the morph. A shape coefficient
  going missing in migration was a real bug in an earlier 4.x, so it is worth a look.
- Morph durations still behave the way they did.

### The multi-track engine

The **Multi-Track Engine** toggle on the Options page is **off by default**, which
reproduces the 3.2 single-track behaviour. Turning it on gives every tracked node its own
clock, duration, curve, end mode and group.

Most of the new surface area is here, so most of the undiscovered bugs probably are too.
Try several tracks with different durations, the loop and ping-pong end modes, and per-track
auto sequences running alongside each other.

### Scripted use

If you drive TDMorph from Python, check the
[API reference](Documentation/PresetManager.md). Several methods were removed or renamed
between 3.2 and 4.x. The
[removed list](Documentation/PresetManager.md#removed-since-32) names each one and its
replacement.

One behavioural change to be aware of: `trackConfig` is now a **per-trigger input, not
session state**. A preset's timing applies to the trigger that loaded it and is then
restored, so loading a preset no longer rewrites your session defaults. If you were reading
`trackConfig` back after a morph started, read the engine's `trackTable` row instead.

### The three new components

They are new to this repository but not new code: they have been running inside
ParameterMorpher and SceneLauncher for months. What is untested is how they behave in
*your* project rather than inside a TDMorph tool.

ListView in particular is meant to be genuinely reusable, so if you build a list with it and
something is awkward or missing, that is worth reporting even if nothing is broken.

---

## What has already been verified

Each component carries its own test harness inside the `.tox`. Pulse **Run Tests** on its
`Tests` base and read `Tests/testResults`.

| Component | Checks |
|---|---|
| PresetManager | 171 |
| PresetInspector | 39, plus 111 in its embedded tree |
| JSONTree | 111 |
| ListView | 127 |

Every one of these was run against the exact files in this branch, loaded fresh into an
empty project, and all passed. That is what the harness covers, which is the engine, the
data model and the widget behaviour. It is not a substitute for someone using the tool.

Each component also ships **empty**: no presets, no stored paths, no example content and no
paths pointing back at a machine that is not yours.

---

## Reporting

Please use the [issue tracker](https://github.com/DarienBrito/TDMorph/issues).

What makes a report easy to act on:

- Which component and which version, from its **About** page.
- Your TouchDesigner build.
- Whether the project came from 3.2, and if so, the JSON export from before the upgrade.
- Whether the multi-track engine was on or off.
- The smallest project that still shows the problem, if you can get there.
- The output of **Run Tests** on the affected component, which says whether the engine
  itself is healthy or the problem is in how it is wired.

Notes on how the tool behaves when something is wrong, since these are easy to mistake for
bugs:

- The PresetManager **Lock** toggle blocks randomization and morphing, and also blocks
  PresetInspector from writing to it.
- PresetInspector edits are **values only**. You cannot add, rename or delete keys from the
  tree. A refused write records its reason in `lastWriteError`.
- A tracked node that has been moved needs **Paths > Update** to re-key its presets, which
  finds it again by its `TDMorphPath` tag.

---

## Going back

The stable release is [3.2.1](https://github.com/DarienBrito/TDMorph/releases/tag/v3.2.1).

Reverting means replacing the component and restoring your pre-upgrade preset JSON. A
project saved after a v2 migration holds v2 presets, and **3.2 cannot read them**. Migration
runs forward only, which is the reason for the backup advice above.
