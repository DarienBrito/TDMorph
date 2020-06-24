# TDMorph

TDMorph is a toolbox for enhanced parametric exploration, preset storage, composition and cueing in the TouchDesigner platform. It is meant to help in creating and performing generative content via various methods and archiving of interesting parameter configurations using a JSON format. Furthermore, the library provides a set of tools that developers can use to create their own custom systems. 

## What can I do with it?

1) Random search of states for parameters on any node or number of nodes.
2) Random morphing between states using various different interpolation curves.
3) Storing and retrieval of any arbitrary number of presets.
4) Control of parameters and transitions with automatically generated UIs.
5) Automatic storing, randomization and transformation of all parameters of arbitrary nodes.
6) Auto-learn MIDI and OSC for every control in the generated UI.
7) Full scripting control of all UI features via high-level commands.
8) Global and local timing controls for every single parameter.
9) Automatic creation of animations from stored presets.
10) Flexible cueing system with follow actions and quantization.
11) Pattern generation via scripting with the Patterns library.
12) Algorithmic cueing via scripts.

And much more!

## How does it work?


The architecture of TDMorph is fully modular in the sense that you can access the core functionality building blocks separately or as a whole. There are therefore various approaches you may take, which can be also interchangeably used. Here the most common:

+ You can create an **ElementsContainer** UI, from where to control your parameters, using widgets and a set of buttons to perform various functions.
+ You can create a **PresetManager** node, which is a UI-less object that allows you to control any arbitrary amount of nodes at once and is the backbone of the engine, suitable for advanced developers who want to make their own systems.
+ You can create a **SceneLauncher** node, which is a UI that lets you create and control presets with follow actions.

## Ok, I want to use it!

Great! TDMorph is a rather deep tool, alhtough the basic functionality is self-evident (I hope). Here a quick overview of the general controls to help you get started, if you cannot wait. For a proper step by step explanation of all features, please refer to the [video tutorials](https://vimeo.com/showcase/6682501).

### Controls overview

#### UI


#### Preset Manager


### Tutorials

If you want to learn everything TDMorph has to offer in a structured manner, please check the following tutorials:

https://vimeo.com/showcase/6682501

### Shortcuts

Please see here the [full list of shortcuts](https://github.com/DarienBrito/TDMorph/blob/master/Help/Shortcuts.md).

## No UI, I just want to code! 

Fair enough :) The philosophy behind the construction of TDMorph is that the UI is "dumb". This means that it is completely decoupled from core functionality, so when you interact with it you are invoking lower level commands that do not know what a button or a slider is, at least not implicitely. There is therefore a plethora of higher and lower level set of commands that you can pass to control all objects in TDMorph, using Python. 

In general, a node in TDMorph has always 2 extensions:

+ Core extension (Core UI-less functionality)
+ UI extension (deals exclusively with operations for UI elements)

### UI extension methods

The first category of commands are to set things in TDMorph via the UI. These do not talk with the core nodes in the system but with the widgets. To give an example: you could locate an *ElementsContainer* in TDMorph and then target a specific element of the UI you want to control, that being a button, a parameter or a widget.

To access an *ElementsContainer* you need to invoke it by number (counting from 1), so assuming you have only 1 *ElementsContainer* in your TDMorph workspace, you can invoke that element using:

```python
elementsContainer = op('TDMorph').GetContainer(1)
```
Now, you can control all the UI elements of that object. So if you would like to change its morphing time via the UI you can do:

```python
elementsContainer.SetUITime(SomeTimeValue)
```

### Core extension methods

The second category of commands are to communicate directly with the objects, not with the UI. These methods are the ones used by the system under the hood, so you can do much more with them. These are meant for more advanced developers that want to build  systems on top of the toolbox. To give an example: you could locate an *ElementsContainer* and then delete it, by doing this:

```python
elementsContainer = op('TDMorph').GetContainer(1)
elementsContainer.Delete()
```

### Methods documentation

For a list of all available methods for all the objects in TDMorph, please refer to the node documentation in the [help files](https://github.com/DarienBrito/TDMorph/blob/master/Help/).

Please read carefully the instructions about architecture in the source code, so you create programs that adhere to the philosophy of TDMorph. This is important because it will be easier to mantain as TDMorph evolves.

### Patterns

Since version 2, TDMorph comes with a "Patterns" library, which I wrote based on the homonimus library in the SuperCollider language. Patterns were conceived in the SuperCollider programming language as a "rich and concise score language for music". See: https://doc.sccode.org/Tutorials/A-Practical-Guide/ 

The need for values generation in TouchDesigner moved me to embrace this idea and further create this library for the TDMorph toolkit and TouchDesigner in General. It is not a port of the original SuperCollider version per se, but more of a reverse engineering, using Python's great support for generators and lazy evaluation.

## Bug reports

Feel free to dig around and please suggest improvements if you see something that could be done better in the networks or the code. Also please get in touch if you see I did something stupid somewhere (which is bound to be the case). To report these, please use the issue tracker in the Github repo:

https://github.com/DarienBrito/TDMorph/issues

## Contributions

You are more than welcome to propose additions to the toolkit. Feel free to build your own tools based on TDMorph and get in touch if you want to propose making them part of the official distribution. Please make sure to check carefully the obligations in the license if you plan to make your work available to others.

## Final thoughts

The motivation to share this tool stems from the wonderful sense of comradery that the TouchDesigner community in general has, 
and by the brilliant philosophy of Derivative https://derivative.ca/, as creators of the TouchDesigner software. I hope that the *ethos* that characterizes TD continues, and that this system helps you in expanding your capabilities as a maker. 

## About the license

Since we are artists/programmers and not lawyers, I trust you will give credit where credit is due and respect the licence: GNU General Public License v3 (GPL-3). See this [link with common questions](https://resources.whitesourcesoftware.com/blog-whitesource/top-10-gpl-license-questions-answered) if you wonder what it implies. This means that if at some point you would like to use this toolbox in a **commercial endeavour for which you do not want to disclose the source code**, you will get in touch first, so a fair arrangement can be made. 

Enjoy!

Darien Brito
https://darienbrito.com/
