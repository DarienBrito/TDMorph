# TDMorph 3.2 (BUILD IN PROGRESS... TO BE OFFICIALLY RELEASED VERY SOON)

Note that there are various differences with previous versions. Please refer to this [video demonstration](https://www.youtube.com/watch?v=qIXt53QVFt8&ab_channel=TouchDesigner) from minute 37, where I explain in detail what those are.

## What is TDMorph?

**TDMorph** is a toolbox designed to enhance **parametric exploration**, **preset storage**, **composition**, and **cueing** within the **TouchDesigner** platform.

It facilitates the creation and performance of **generative content** through various methods, while allowing you to **archive and recall parameter configurations** using a flexible **JSON-based format**.

In addition, TDMorph includes a set of **developer tools** for building **custom systems**, making it a versatile resource for artists and technical creators alike.


## What can I do with it?

With **TDMorph**, you can perform a wide range of operations for creative exploration, performance, and system design in **TouchDesigner**, including:

1. **Random search** for parameter states across one or multiple nodes.  
2. **Morphing between states** using various interpolation curves.  
3. **Store and retrieve** an unlimited number of presets.  
4. **Control parameters and transitions** through automatically generated UIs.  
5. **Automatically store, randomize, and transform** parameters of any node.  
6. **Auto-learn MIDI and OSC** mappings for every UI control.  
7. **Script full UI behavior** via high-level Python commands.  
8. **Set global and local timing** for each parameter independently.  
9. **Automatically generate animations** from stored presets.  
10. **Build flexible cueing systems** with follow actions and quantization.  
11. **Generate parameter patterns** programmatically using the *Patterns* library.  
12. **Create algorithmic cueing systems** through scripting.

And much more!

## How does it work?

The architecture of **TDMorph** is fully modular, allowing you to use its core functionality either as a unified system or as individual components. This flexibility lets you combine different approaches depending on your needs.  
The three main modes of operation are:

- **PresetManager**  
  A UI-less core component that manages any number of nodes simultaneously. It serves as the backbone of the engine—ideal for advanced developers who want to build their own systems from scratch.

- **ParameterMorpher**  
  A node with an interactive interface that includes widgets and control buttons, allowing you to easily perform morphing, randomization, and parameter operations across multiple nodes.

- **SceneLauncher**  
  A high-level UI designed for show control. It enables you to organize and trigger scenes and presets, supports follow actions, and integrates seamlessly with cue-based workflows.

## Tutorials

**TDMorph** is a powerful and versatile tool — while it may take some time to explore its depth, the basic functionality is intuitive and easy to grasp.

To get started and learn everything TDMorph has to offer, check out this 👉 [**Tutorial series** on Vimeo](https://vimeo.com/showcase/6682501)

### Overview

Here a quick overview of the main tools to give you a quick idea. 

#### Preset Manager

UI-less node to store, recall, and morph parameter states across multiple TouchDesigner nodes. The core of the TDMorph architecture.

<img src="https://github.com/DarienBrito/TDMorph/blob/master/imgs/1.jpg" width="800">

#### Parameter Morpher

A powerful drag-and-drop front end for generating automatic UIs, enabling morphing, preset management, and aleatoric parameter exploration — fully

<img src="https://github.com/DarienBrito/TDMorph/blob/master/imgs/2.jpg" width="800">

#### Scene Launcher

A minimalistic controller for cueing and managing scenes from arbitrary presets, featuring follow actions, randomization, and versatile tools for intuitive scene sequencing. 

<img src="https://github.com/DarienBrito/TDMorph/blob/master/imgs/3.jpg" width="800">

# Shortcuts

The **TDMorph** ecosystem includes a set of simple, intuitive shortcuts designed to streamline your workflow. You only need to remember a few combinations — all built around the keys:

<kbd>Shift</kbd> or <kbd>Ctrl</kbd> + <kbd>Mouse Button</kbd>

That’s it! Every shortcut in TDMorph is derived from these two simple modifiers.

## ElementsContainer

### When clicking on a preset slot

- <kbd>Shift</kbd> + <kbd>Left Click</kbd> — Store a preset  
- <kbd>Shift</kbd> + <kbd>Right Click</kbd> — Delete a preset  
- <kbd>Shift</kbd> + <kbd>Middle Click</kbd> — Freeze a preset  
- <kbd>Ctrl</kbd> + <kbd>Left Click</kbd> — Jump to preset (no interpolation)  
- <kbd>Ctrl</kbd> + <kbd>Right Click</kbd> — Morph to preset in 1 second (for quick transition checks)

### When clicking on an element’s name

- <kbd>Shift</kbd> + <kbd>Left Click</kbd> — Reset element to its original value (on creation)  
- <kbd>Shift</kbd> + <kbd>Right Click</kbd> — Rename element

### When clicking on a container’s name

- <kbd>Shift</kbd> + <kbd>Right Click</kbd> — Rename container

### When clicking on empty space within an element’s container

- <kbd>Right Click</kbd> — Open a context menu with various available actions


## ScenesLauncher

### When clicking on empty space within the Scene Launcher

- <kbd>Right Click</kbd> — Open a context menu with various available actions


## MIDI and OSC

### When either is enabled

- <kbd>Left Click</kbd> — Activate auto-learning (waits for a MIDI or OSC input to map)  
- <kbd>Right Click</kbd> — Assign the parameter to the detected MIDI or OSC signal  
- <kbd>Middle Click</kbd> — Remove the MIDI or OSC mapping


## Code documentation

To be done...

## Patterns

Since version 2, **TDMorph** includes a **Patterns** library — inspired by the *homonymous* system in the **SuperCollider** language. Originally, *Patterns* were conceived in SuperCollider as *“a rich and concise score language for music.”*  
You can read more about this concept here: [SuperCollider Practical Guide](https://doc.sccode.org/Tutorials/A-Practical-Guide/)

The motivation behind this library was the need for a powerful **value generation system** within TouchDesigner. Rather than a direct port, this implementation is a **reverse-engineered adaptation** of SuperCollider’s original Patterns system — built from the ground up using Python’s **generators** and **lazy evaluation** capabilities.

The result is a flexible and expressive framework for **algorithmic pattern generation**, designed to integrate seamlessly with the **TDMorph** toolkit and the **TouchDesigner** environment.


## Bug Reports

Feedback and contributions are always welcome! If you notice anything that could be improved — whether in the networks, the UI, or the underlying code — please don’t hesitate to let me know. And if you spot something that looks off (which is bound to happen here and there), I’d really appreciate your input.

To report bugs or suggest improvements, please use the official issue tracker:

🔗 [**TDMorph GitHub Issues**](https://github.com/DarienBrito/TDMorph/issues)


## Contributions

Contributions are highly encouraged! You’re welcome to build your own tools on top of **TDMorph** and share your ideas or improvements with the community.

If you’d like to propose integrating your work into the official distribution, feel free to **get in touch**.  

Before sharing or publishing your work, please make sure to **review the license terms** to ensure compliance with its requirements.

Together, we can keep expanding and refining the TDMorph ecosystem. 🚀


## Support

Thank you for your interest in my work! 🙏 You can follow me on [**Instagram**](https://www.instagram.com/darien.brito/).

If you’d like to go one step further in supporting what I do, consider subscribing to my [**Patreon**](https://www.patreon.com/c/darienbrito). Your support helps me keep creating, maintaining tools, and sharing knowledge with the community. 💛


## Final Thoughts

The motivation to share this tool comes from the wonderful sense of **camaraderie** within the **TouchDesigner** community, and from the inspiring philosophy of its creators at [**Derivative**](https://derivative.ca/).

I hope the *ethos* that defines the TouchDesigner world continues to thrive, and that **TDMorph** helps you expand your creative possibilities as an artist, technologist, and maker.


## About the License

Since we are artists and programmers — not lawyers — I trust you’ll give credit where it’s due and respect the license: **GNU General Public License v3 (GPL-3)**.

If you’re unsure what this implies, you can read this helpful overview: [**Top 10 GPL License Questions Answered**](https://resources.whitesourcesoftware.com/blog-whitesource/top-10-gpl-license-questions-answered)

In short, if you wish to use any part of this toolbox in a **commercial project** where you **do not intend to disclose the source code**, please get in touch first so we can agree on a **fair arrangement**. 🤝

Enjoy!

Darien Brito
https://darienbrito.com/
