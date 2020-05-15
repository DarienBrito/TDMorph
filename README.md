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

Fair enough :) The philosophy behind the construction of TDMorph is that the UI is "dumb". This means that it is completely decoupled from the core functionality, so when you interact with it you are invoking lower level commands that do not know what a button or a slider is, at least not implicitely. There is therefore a high level set of commands that you can pass to control it, using Python. 

## UI-level commands

The first category of commands are to control UI elements. These do not talk with the core nodes in the system but with the widgets. In order to access these, you first need to locate an *ElementsContainer* and then target a specific element of the UI you want to control, that being a button, a parameter or a widget.

To access an *ElementsContainer* you need to invoke it by number (counting from 1), so assuming you have only 1 *ElementsContainer* in your TDMorph workspace, you can invoke that element using:

```python
elementsContainer = op('TDMorph').GetContainer(1)
```
Now, you can control all the UI elements of that object. So if you would like to change its morphing time via the UI you can do:

```python
elementsContainer.SetUITime(SomeTimeValue)
```
### *Elements Container* Methods

Here all the methods available for an *ElementsContainer*:

```python
SetUIDistribution(str)    # Changes the random distribution (Uniform, Normal, Beta)
SetUIInterpolation(str)   # Changes the moprhing curve (Linear, Scurve, etc)

SetUIGlobal(bool)         # Enables local/global behaviour
ClickUISync()             # Enables local/global clock syncing 
SetUIAuto(bool)           # Enables automatic behaviour

SetUIMorphs(int)          # Sets the amount of morphings
SetUITime(float)          # Sets the morphing time

ClickUISequence()         # Clicks the preset sequence button

ClickUIRandomize()        # Clicks the randomize button

ClickUIMorph()            # Clicks the morph button

UIImportPreset()           # Triggers importing a preset
UIExportPreset()           # Triggers exporting a preset

ClickUISubPreset()        # Substracts one preset slot
ClickUIAddPreset()        # Adds one preset slot
SetUINumPresets(int)      # Changes the number of preset slots
ClickUIClearPresets()     # Clears all presets

SetUISetPreset(int)       # Sets preset n 
SetUIStorePreset(int)     # Stores a preset in n slot
SetUIUnstorePreset(int)   # Removes a preset from n slot 

GetElement(int)            # Returns a widget from the container
```
The last method in the list returns the targeted widget. Like with the container, you may get a widget by asking for a slider number. Assuming you want to get the first widget in your container, you may access it like:

```python
element = elementsContainer.GetElement(1) 
```

Then, if you would like to change the element you need to do:

```python
element.SetUIElementValue(SomeValue)
```

### Element Methods

Here all the methods available for elements:

```python
SetUIElementValue(float)     # Sets the value for the widget
ClickUIElementRandomize()    # Triggers widget's randomization
ClickUIElementInterpolate()  # Triggers widget's morphing
SetUIElementLock(bool)       # Sets lock status
SetUIElementReveal()     	   # Enables deep parameters reveal
ClickUIElementDestroy()      # Destroys widget
SetUIElementDistribution(str)  # Sets random distribution (Uniform, Normal, Beta)
SetUIElementInterpolation(int) # Sets morphing curve (Linear, Scurve, Exponential, etc)
SetUIElementTime(float)        # Sets morphing time
SetUISnap(int) 				         # Sets the snapping action for non-interpolatable parameters
```

## Object level commands

When doing more advanced tasks it is perhaps necessary to access the methods from objects direcly, for instance if you are working with a *PresetManager* or if you want to interact and retrieve information from the level of the inner classes of the objects. There are numerous things you can do with the objects, I describe here only the most common:

### ElementsContainer

### PresetManager

### PresetCompoer

### Patterns

TDMorph comes with a "Patterns" library, which I wrote based on the homonimus library in the SuperCollider language. Patterns were conceived in the SuperCollider programming language as a "rich and concise score language for music". See: https://doc.sccode.org/Tutorials/A-Practical-Guide/ 

The need for values generation in TouchDesigner moved me to embrace this idea and further create this library for the TDMorph toolkit and TouchDesigner in General. Mine is not a port per se, but more of a reverse engineering of the original, since Python's support for generators and lazy evaluation is so nice :) 

### Deeper methods

It is fair to assume that If you have the need to access lower level methods, you are proficient enough to figure out for yourself the inner structure of the Classes. In general, a node in TDMorph has always 2 extensions:

+ Core extension (Core UI-less functionality)
+ UI extension (deals exclusively with operations for UI elements)

Please read carefully the instructions about architecture in the source code, so you create programs that adhere to the philosophy of TDMorph.

## Bug reports

Feel free to dig around and please suggest improvements if you see something that could be done better in the networks or the code. Also please get in touch if you see I did something stupid somewhere (which is bound to be the case). To report these, please use the issue tracker in the Github repo:

https://github.com/DarienBrito/TDMorph/issues

## Contributions


## Final thoughts

The motivation to share this tool stems from the wonderful sense of comradery that the TouchDesigner community in general has, 
and by the brilliant philosophy of Derivative https://derivative.ca/, as creators of the TouchDesigner software. I hope that the *ethos* that characterizes TD continues, and that this system helps you in expanding your capabilities as a maker. 

## About the license

Since we are artists/programmers and not lawyers, I trust you will give credit where credit is due and respect the licence: GNU General Public License v3 (GPL-3). See this (link with common questions) if you wonder what this implies. https://resources.whitesourcesoftware.com/blog-whitesource/top-10-gpl-license-questions-answered This means that if at some point you would like to use this tool in a commercial endeavour for which you do not want to disclose the source code, you will get in touch first, so a fair arrangement can be made. 

Enjoy!

Darien Brito
https://darienbrito.com/
