# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.0.1] - 2020-02-10
### Added

- Marker to show preset storage within the preset buttons
- Implemented a "pin" button, to collapse menu to just preset control for workflow enhancement
- Now its possible to change range of sliders to any arbitrary set of values
- Non interpolating parameters such as menus will change on start of trigger
- On completion signal for morphings is now exposed to the user
- Clocks for each slider are now exposed to the user
- Support for menu parameters, where range of slider is the number of items in menu
- Refactoring of SliderUI class to use properties (like it should)
- Deletion of unnecessary methods in SliderContainer and SliderUI classes
- Syncing affects also random distribution and interpolation curves

### Enhancements

- Now possible to rename parameters by double-clicking on the name
- To save a preset shift-lclick, to delete it shift-rclick on the preset button
- Got rid of unnecesary  buttons for recall and save of presets
- Got rid of global shortcut for Lib. This allows for multiple instances of TDMorph in the same patch
- Binding is now from sliders to parameter instead of the other way around
- Attribute conversion for some methods, making the code more consistent
- Enhanced flow for changing parameters, more clear for developers

## [Released]

## [1.0.0] - 2019-31-12
- First official release
