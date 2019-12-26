# TDMorph

TDMorph is a toolbox for enhanced parametric exploration in the TouchDesigner platform. It is meant to help in creating generative content via various methods and sharing of interesting parameter configurations among users using a JSON format.  

![alt text](https://github.com/DarienBrito/TDMorph/blob/master/imgs/CaptureUITDMorph.PNG)

## What can I do with it?

1) Random search of states for parameters on any node using various different distributions.
2) Random morphing between states using various different interpolation curves.
3) Storing and retrieval of any arbitrary number of presets.
4) Control of parameters with an automatically generated UI.
5) Automatic storing, randomization and transformation of all parameters of arbitrary nodes.
6) Auto-learn MIDI and OSC for every control in the generated UI.
7) Fulls scripting control of all features via high-level commands.
8) Global and local controls for every single parameter.

## How does it work?

There are two main approaches you may take:

+ You can create a UI from where to control your parameters, using sliders and a set of buttons that perform various functions.
+ You can create a Preset Manager node, which does everything the UI does but with a slightly different paradigm.

## Ok, I want to use it!

Great! Please check the following tutorials to learn all the features in a structured manner:

## Nah, I just want to code! 

Fair enough :) The philosophy behind the construction of TDMorph is that the UI is "dumb". This means that it is completely decoupled from the core functionality, so when you interact with it you are invoking lower level commands that do not know what a button or a slider is, at least not implicitely. There is therefore a high level set of commands that you can pass to control the UI using Python. In order to access those, you first need to locate a sliders container and then target a specific element of the UI you want to control, that being a button, a parameter or a slider.

To access a sliders container, you need to invoke it by number, so assuming you have only 1 slider container in your TDMorph workspace, you can invoke that element using:

```python
sliderContainer = op('TDMorph').GetContainer(1)
```
Now, you can control all the UI elements of that object. So if you would like to change its morphing time you can do:

```python
sliderContainer.SetUITime(SomeTimeValue)
```

### Sliders Container Methods

Here all the methods available for a sliders container:

```python
SetUIDistribution(int)    
SetUIInterpolation(int)
SetUIGlobal(bool)
SetUISync(bool)
SetUIAuto(bool)
SetUIMorphs(int)
SetUITime(float)
SetUISequence(int)
SetUIRandomize(int)
SetUIMorph(int)
SetUIImport(int)
SetUIExport(int)
SetUISubPreset(int)
SetUINumPresets(int)      # 
SetUIClearPresets(int)    # Clears all presets
SetUISetPreset(int)       # Sets a preset (morphing)
SetUIStorePreset(int)     # Stores a preset in a slot
SetUIUnstorePreset(int)   # Removes a preset from a slot 

GetSlider(int)            # Returns a slider from the container
```



here documentation of all relevant methods

```python
print(x) 
```



