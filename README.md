# TDMorph

TDMorph is a toolbox for enhanced parametric exploration, preset storage, composition and cueing in the TouchDesigner platform. It is meant to help in creating and performing generative content via various methods and archiving of interesting parameter configurations using a JSON format. Furthermore, the library provides a set of tools that developers can use to create their own custom systems. 

![alt text](https://github.com/DarienBrito/TDMorph/blob/master/imgs/TDMorphCapture.PNG)

## What can I do with it?

1) Random search of states for parameters on any node or number of nodes.
2) Random morphing between states using various different interpolation curves.
3) Storing and retrieval of any arbitrary number of presets.
4) Control of parameters with an automatically generated UI.
6) Auto-learn MIDI and OSC for every slider in the generated UI.
7) Full scripting control of all UI features via high-level commands.
8) Global and local timing controls for every single parameter.
9) Automatic creation of animations from stored presets.
10) Flexible cueing system with follow actions and quantization.
11) Pattern generation via scripting with the Patterns library

## How does it work?

There various approaches you may take interchangeably. Here the most common:

+ You can create an *ElementsContainer* UI, from where to control your parameters, using widgets and a set of buttons to perform various functions.
+ You can create a *PresetManager* node, which is a UI-less object that allows you to control any arbitrary amount of nodes at once.
+ You can create a *PresetComposer* node, which is a UI that lets you create and control presets with follow actions.

## Ok, I want to use it!

Great! Here a quick overview of the general controls. I hint here at what the more misterious elements in the UI do, hopefully the rest is self-explanatory. For a proper step by step explanation, refer to the video tutorials below.

### Controls overview

#### UI

![alt text](https://github.com/DarienBrito/TDMorph/blob/master/imgs/TDMorphSlidersControls.png)

![alt text](https://github.com/DarienBrito/TDMorph/blob/master/imgs/SliderControls.png)

#### Preset Manager

![alt text](https://github.com/DarienBrito/TDMorph/blob/master/imgs/TDMorphPrestManagerControls.png)

### Tutorials

Please check the following tutorials to learn all the features in a structured manner:

https://vimeo.com/showcase/6682501

## No UI, I just want to code! 

Fair enough :) The philosophy behind the construction of TDMorph is that the UI is "dumb". This means that it is completely decoupled from the core functionality, so when you interact with it you are invoking lower level commands that do not know what a button or a slider is, at least not implicitely. There is therefore a combination of high and lower level set of commands that you can pass to control all objects in TDMorph, using Python. 

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

The second category of commands are to communicate directly with the objects, not with the UI. These methods are the ones used by the system under the hood, so you can do much more. To give an example: you could locate an *ElementsContainer* and then delete it, by doing this:

```python
elementsContainer = op('TDMorph').GetContainer(1)
elementsContainer.Delete()
```

### Commands documentation

For a list of all available methods for all the objects in TDMorph, please refer to the node documentation in the [help files](https://github.com/DarienBrito/TDMorph/blob/master/Help/)

Please read carefully the instructions about architecture in the source code, so you create programs that adhere to the philosophy of TDMorph.

### Patterns

Since version 2, TDMorph comes with a "Patterns" library, which I wrote based on the homonimus library in the SuperCollider language. Patterns were conceived in the SuperCollider programming language as a "rich and concise score language for music". See: https://doc.sccode.org/Tutorials/A-Practical-Guide/ 

The need for values generation in TouchDesigner moved me to embrace this idea and further create this library for the TDMorph toolkit and TouchDesigner in General. It is not a port of the original version per se, but more of a reverse engineering, using Python's great support for generators and lazy evaluation.

## Bug reports

Feel free to dig around and please suggest improvements if you see something that could be done better in the networks or the code. Also please get in touch if you see I did something stupid somewhere (which is bound to be the case). To report these, please use the issue tracker in the Github repo:

https://github.com/DarienBrito/TDMorph/issues

## Contributions

You are more than welcome to propose additions to the toolkit. Feel free to build your own tools based on TDMorph and get in touch if you want to propose making them part of the official distribution. Please make sure to check carefully the obligations in the license if you plan to make your work available to others.

## Final thoughts

The motivation to share this tool stems from the wonderful sense of comradery that the TouchDesigner community in general has, 
and by the brilliant philosophy of Derivative https://derivative.ca/, as creators of the TouchDesigner software. I hope that the *ethos* that characterizes TD continues, and that this system helps you in expanding your capabilities as a maker. 

## About the license

Since we are artists/programmers and not lawyers, I trust you will give credit where credit is due and respect the licence: GNU General Public License v3 (GPL-3). See this [link with common questions](https://resources.whitesourcesoftware.com/blog-whitesource/top-10-gpl-license-questions-answered) if you wonder what it implies. This means that if at some point you would like to use this tool in a commercial endeavour for which you do not want to disclose the source code, you will get in touch first, so a fair arrangement can be made. 

Enjoy!

Darien Brito
https://darienbrito.com/
