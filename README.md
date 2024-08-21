# TDMorph 3.1.1 (alpha)

Please note that some things still need work, including documentation and such. This release is in alpha version, very close to an official release. I greatly appreciate your input in helping me find all left over bugs, so I can move to an official version as soon as possible. 

Note that there are some differences with previous versions. Please refer to this [video demonstration](https://www.youtube.com/watch?v=qIXt53QVFt8&ab_channel=TouchDesigner) from minute 37, where I explain in detail what those are.

## What is TDMorph?

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

The architecture of TDMorph is fully modular, allowing you to access the core functionality as a whole or as separate building blocks. There are therefore various approaches you may take, which can be also interchangeably used. Here the most obvious:

+ You can create a **PresetManager** which is a UI-less object that allows you to control any arbitrary amount of nodes at once and is the backbone of the engine, suitable for advanced developers who want to make their own systems.
+ You can create a **ParameterMorpher** node, and use widgets and a set of buttons to perform various functions over any amount of parameters with ease.
+ You can create a **SceneLauncher** node, which is a UI that lets you create and control scenes and presets with follow actions, suitable for show control.

## Ok, I want to use it!

Great! TDMorph is a rather deep tool and requires some exploration to master but the basic functionality should be self-evident. Please check the [full collection of tutorials](https://vimeo.com/showcase/6682501) to learn everything TDMorph has to offer in a structured manner.

### Overview

Here a quick overview of the general controls to give you a quick idea. 

#### Preset Manager

 <img src="https://github.com/DarienBrito/TDMorph/blob/master/imgs/PresetManager.PNG" width="800">

#### ParameterMorpher

![Header](https://github.com/DarienBrito/TDMorph/blob/master/imgs/TDMorph%20header.svg)

#### Scene launcher

![Header](https://github.com/DarienBrito/TDMorph/blob/master/imgs/SceneLauncher.svg)

# Shortcuts

There are various shortcuts in the TDMorph ecosystem. I have tried to keep them as simple as possible, so the only keys you will ever have to remember are <kbd>Shift</kbd> or <kbd>Ctrl</kbd> + <kbd>Mouse button</kbd>.

## ElementsContainer

### When pressing over a preset slot

* <kbd>shift</kbd> + <kbd>left click</kbd> = store a preset
* <kbd>shift</kbd> + <kbd>right click</kbd> = delete a preset
* <kbd>shift</kbd> + <kbd>middle click</kbd> = freeze a preset
* <kbd>ctrl</kbd> + <kbd>left click</kbd> = jump to preset (no interpolation)
* <kbd>ctrl</kbd> + <kbd>righ click</kbd> = morph to preset in 1 second (meant for quick transition check)

### When pressing over an element's name 

* <kbd>shift</kbd> + <kbd>left click</kbd> = set the element to value found on creation
* <kbd>shift</kbd> + <kbd>right click</kbd> = change element's name

### When pressing over an container's name 

* <kbd>shift</kbd> + <kbd>right click</kbd> = change element's name

### When pressing on an element's container empty space

* <kbd>right click</kbd> = reveal menu with various actions to take

## ScenesLauncher

### When pressing on a Scenes Launhcer empty space

* <kbd>right click</kbd> = reveal menu with various actions to take

## MIDI and OSC

### When either is enabled

* <kbd>left click</kbd> = activate auto-learning (expects a MIDI or OSC change to map it)
* <kbd>right click</kbd> = sets the parameter to the learned MIDI or OSC signal
* <kbd>middle click</kbd> = deletes the MIDI or OSC mapping

## Code documentation

To be done...

## Patterns

Since version 2, TDMorph comes with a "Patterns" library, which I wrote based on the homonimus library in the SuperCollider language. Patterns were conceived in the SuperCollider programming language as a "rich and concise score language for music". See: https://doc.sccode.org/Tutorials/A-Practical-Guide/ 

The need for values generation in TouchDesigner moved me to embrace this idea and further create this library for the TDMorph toolkit and TouchDesigner in General. It is not a port but a reverse engineering of the original SuperCollider version, using Python's great support for generators and lazy evaluation.

## Bug reports

Feel free to dig around and please suggest improvements if you see something that could be done better in the networks or the code. Also please get in touch if you see I did something stupid somewhere (which is bound to be the case). To report these, please use the issue tracker in the Github repo:

https://github.com/DarienBrito/TDMorph/issues

## Contributions

You are more than welcome to propose additions to the toolkit. Feel free to build your own tools based on TDMorph and get in touch if you want to propose making them part of the official distribution. Please make sure to check carefully the obligations in the license if you plan to make your work available to others.

## Support

Thank you for your interest in my work! Is nice already if you can follow me on [Instagram](https://www.instagram.com/darien.brito/) and [Twitter](https://twitter.com/DarienBrito)

If you would like to go one step further with your support, I highly encourage you to make a donation to one of the following organizations. They are doing important and urgent work and need your donation more than I do:

[Refugees International](https://www.refugeesinternational.org/) | [Coalition for Rainforest Nations](https://www.rainforestcoalition.org/) | [Amazon Frontlines](https://amazonfrontlines.org/) | [Wikipedia](https://donate.wikimedia.org/w/index.php?title=Special:LandingPage&country=NL&uselang=en&utm_medium=spontaneous&utm_source=fr-redir&utm_campaign=spontaneous)

## Final thoughts

The motivation to share this tool stems from the wonderful sense of comradery that the TouchDesigner community in general has
and by the brilliant philosophy of Derivative https://derivative.ca/, as creators of the TouchDesigner software. I hope that the *ethos* that characterizes TD continues and that this system helps you in expanding your capabilities as a maker. 

## About the license

Since we are artists/programmers and not lawyers, I trust you will give credit where credit is due and respect the licence: GNU General Public License v3 (GPL-3). See this [link with common questions](https://resources.whitesourcesoftware.com/blog-whitesource/top-10-gpl-license-questions-answered) if you wonder what it implies. This means that if at some point you would like to use any part of this toolbox in a **commercial endeavour for which you do not want to disclose the source code**, you will get in touch first, so a fair arrangement can be made. 

Enjoy!

Darien Brito
https://darienbrito.com/
