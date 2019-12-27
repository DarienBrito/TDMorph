# TDMorph

TDMorph is a toolbox for enhanced parametric exploration in the TouchDesigner platform. It is meant to help in creating generative content via various methods and sharing of interesting parameter configurations among users using a JSON format.  

![alt text](https://github.com/DarienBrito/TDMorph/blob/master/imgs/TDMorphCapture.PNG)

## What can I do with it?

1) Random search of states for parameters on any node using various different distributions.
2) Random morphing between states using various different interpolation curves.
3) Storing and retrieval of any arbitrary number of presets.
4) Control of parameters with an automatically generated UI.
5) Automatic storing, randomization and transformation of all parameters of arbitrary nodes.
6) Auto-learn MIDI and OSC for every control in the generated UI.
7) Full scripting control of all features via high-level commands.
8) Global and local controls for every single parameter.

## How does it work?

There are two main approaches you may take:

+ You can create a UI from where to control your parameters, using sliders and a set of buttons that perform various functions.
+ You can create a Preset Manager node, which does everything the UI does but with a slightly different paradigm.

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

## No UI, I just want to code! 

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
SetUIDistribution(int)    # Changes the random distribution
SetUIInterpolation(int)   # Changes the moprhing curve

SetUIGlobal(bool)         # Enables local/global behaviour
SetUISync(bool)           # Enables local/global clock syncing 
SetUIAuto(bool)           # Enables automatic behaviour

SetUIMorphs(int)          # Sets the amount of morphings
SetUITime(float)          # Sets the morphing time

ClickUISequence()         # Clicks the preset sequence button
SetUISequence(bool)       # Sets the preset sequence button on/off

ClickUIRandomize()        # Clicks the randomize button
SetUIRandomize(bool)      # Sets the randomize button on/off

ClickUIMorph()            # Clicks the morph button
SetUIMorph(bool)          # Sets the morph button on/off

ClickUIImport()           # Triggers importing a preset
ClickUIExport()           # Triggers exporting a preset

ClickUISubPreset()        # Substracts one preset slot
ClickUIAddPreset()        # Adds one preset slot
SetUINumPresets(int)      # Changes the number of preset slots
ClickUIClearPresets()     # Clears all presets

SetUISetPreset(int)       # Sets preset n 
SetUIStorePreset(int)     # Stores a preset in n slot
SetUIUnstorePreset(int)   # Removes a preset from n slot 

GetSlider(int)            # Returns a slider from the container
```
The last method returns the targeted slider. Like with the container, you may get a slider by asking for a slider number. Assuming you have only 1 slider in your container, you may access it like:

```python
slider1 = sliderContainer.GetSlider(1) 
```

Then, if you would like to change the slider value for instance, you need to do:

```python
slider1.SetUISliderValue(SomeValue)
```

### Sliders Methods

Here all the methods available for sliders:

```python
SetUISliderValue(float)     # Sets the value for the slider
ClickUISliderRandomize()    # Triggers slider's randomization
ClickUISliderInterpolate()  # Triggers slider's morphing
SetUISliderLock(bool)       # Sets lock status
SetUISliderReveal(bool)     # Enables deep parameters reveal
ClickUISliderDestroy()      # Destroys slider
SetUISliderDistribution(int)  # Sets random distribution
SetUISliderInterpolation(int) # Sets morphing curve
SetUISliderTime(float)        # Sets morphing time
```

### Deeper methods

It is fair to assume that If you have the need to access lower level methods, you are proficient enough to figure out for yourself the inner structure of the Classes. A node in TDMorph in general has always 2 extensions:

+ Core extension (Core UI-less functionality)
+ UI extension (deals exclusively with operations with UI elements)

Feel free to look around and please suggest improvements if you see something that could be done better, or if I did some stupid thing (which is more than probable to be the case) 

## Final thoughts

The motivation to share this tool stems from the wonderful sense of comradery that the TouchDesigner community in general has, 
and by the brilliant philosophy of Derivative, as creators of the TouchDesigner software. I hope that the *ethos* that characterizes TD continues, and that this small contribution helps you in expanding your capabilities as a maker. 

Since we are artists/programmers and not lawyers, I trust you will give credit where credit is due and respect the licence, meaning that if at some point you would like to use this tool in a commercial endeavour, you will get in touch first :)

Enjoy!

Darien Brito
https://darienbrito.com/
