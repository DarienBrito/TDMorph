## ElementsContainer

### When clicking on a preset slot

- <kbd>Left Click</kbd> — Recall the preset, morphing over its own stored time and curve  
- <kbd>Shift</kbd> + <kbd>Left Click</kbd> — Store a preset, or overwrite the one in that slot  
- <kbd>Shift</kbd> + <kbd>Right Click</kbd> — Delete a preset  
- <kbd>Shift</kbd> + <kbd>Middle Click</kbd> — Freeze or unfreeze. Locks interaction with the elements so they cannot be nudged by accident. Stored slots only  
- <kbd>Ctrl</kbd> + <kbd>Left Click</kbd> — Jump to preset (no interpolation)  
- <kbd>Ctrl</kbd> + <kbd>Right Click</kbd> — Morph over the container's global **Morph Time** instead of the preset's stored time, for a quick transition check  
- <kbd>Alt</kbd> + drag one slot onto another — Swap which preset each button triggers. Both slots must be stored. *Rename presets in order* bakes the new order into storage

### When clicking on an element’s name

- <kbd>Shift</kbd> + <kbd>Left Click</kbd> — Reset element to the value and range it had on creation  
- <kbd>Shift</kbd> + <kbd>Right Click</kbd> — Rename element  
- <kbd>Alt</kbd> + drag one element onto another — Swap their positions

### When clicking on a container’s name

- <kbd>Shift</kbd> + <kbd>Right Click</kbd> — Rename container

### When clicking on empty space within an element’s container

- <kbd>Right Click</kbd> — Open a context menu: *Reset parameters*, *Clear parameters*, *Rename presets in order*, *Add script*


## SceneLauncher

Also available inside the component: click the **?** icon in the header, or the **Shortcuts**
pulse on the Config page. Everything here is mouse only, with no modifier keys.

### Scene list (the wide list on the left)

- <kbd>Left Click</kbd> the **Go** icon — Launch the scene. A scene launches from this icon and
  nowhere else, so clicking any other cell can never fire a transition
- <kbd>Left Click</kbd> the colour chip — Open the colour picker on that scene
- <kbd>Left Click</kbd> the bin icon — Delete the scene (asks first)
- <kbd>Left Click</kbd> twice on **Scene**, **Length**, **Delay** or **Script** — Edit in place.
  The first click selects and arms the cell, the second opens the editor. *Editing Length also
  overwrites the stored time inside the scene's Target preset*, unless the target is **None**
- <kbd>Right Click</kbd> on **Target**, **Curve** or **Action** — Open that cell's menu. Target
  lists the attached PresetManager's presets, Curve the morph curves, Action the follow
  actions. *Picking a Curve also overwrites the stored curve inside the Target preset*
- Press a row and release on another — Re-order the scenes. The transport cue follows the row
  it was on
- <kbd>Right Click</kbd> on empty space — New scene, Duplicate, Clear scenes, Clear actions,
  Clear scripts, Export presets, Import presets, Refresh. Duplicate copies the selected row,
  falling back to the last launched scene
- **Delay** and **Script** appear only while *Enable delays* and *Enable scripting* are on

### Preset list (the narrow list on the right)

Its contents live in the attached PresetManager, so with none attached the list is empty.

- <kbd>Left Click</kbd> — Select the preset. The selected row is what a drag onto the scene
  list carries
- <kbd>Left Click</kbd> twice on the name — Rename. Every scene aiming at it follows the new name
- <kbd>Left Click</kbd> the bin icon — Delete (asks first). Every scene aiming at it drops back
  to **None**
- <kbd>Right Click</kbd> on a preset — New preset, Clear presets, Overwrite preset
- <kbd>Right Click</kbd> on empty space — New preset, Clear presets, Refresh
- Press a row and release on another — Re-order. Release on the **scene list** instead and a
  new scene is created aiming at the dragged preset, after asking for a name

### Both lists

- <kbd>Right Click</kbd> a column heading — Rename, Left, Center, Right. Only while the list
  has rows
- Press the border between two headings and drag — Resize the column. The cursor changes when
  you are on it
- <kbd>Left Click</kbd> below the rows — Clear the selection

### Header

- **Settings** and **Look** open their parameter popups
- **Map** enters or leaves map mode, and appears once a MIDI or an OSC input is wired on the
  Inputs page
- The two remaining toggles show or hide the **Follow action** and **Morph** sections
- **?** opens the mouse and key reference

## MIDI and OSC

Since 4.5.0 there is one **Map** mode for both protocols and one mapping list. The Map icon
appears in the header once a MIDI or an OSC input is wired on the Inputs page.

1. Turn on **Map**. Every mappable control shows a badge, and already-mapped controls are
   badged differently from free ones.
2. **Click** a badge to arm that control (any mouse button). Its badge blinks while it
   listens. Click it again to disarm.
3. Move a fader, knob or key. It binds to the armed parameter. Learning the same control
   again moves the mapping rather than stacking a second one.
4. Edit or remove mappings in **Manage Mappings**: per-mapping **Min** and **Max**, and
   **jump** or **pickup** takeover. A row marked *(missing)* points at a control that is
   gone, and **Prune Dead Mappings** clears those.
