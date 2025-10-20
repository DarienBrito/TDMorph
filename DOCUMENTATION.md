| **Property**          | **Type** | **Description**                                                                 |
|------------------------|----------|---------------------------------------------------------------------------------|
| `Presets`              | `dict`   | Dictionary of stored presets. Each preset contains parameter states, morph time, curve, and random distribution. |
| `AutoMode`             | `bool`   | Enables automatic randomization or morphing.                                   |
| `CurrentPresetName`    | `str`    | The currently selected preset name.                                            |
| `CurrentMorphCounter`  | `int`    | The current morph iteration count.                                             |
| `LoopSequenceStatus`   | `bool`   | Enables looping through preset sequences.                                      |
| `RandomDistribution`   | `str`    | The random distribution function used by the morpher.                          |
| `NumMorphs`            | `int`    | Number of morph steps per transition.                                          |
| `MorphTime`            | `float`  | Time (in seconds) for a morph transition.                                      |
| `MorphCurve`           | `str`    | Type of interpolation curve used.                                              |
| `Blend`                | `float`  | Blend factor for mixing presets.                                               |
| `BlendingActive`       | `bool`   | Indicates if blending between presets is active.                               |
| `Lock`                 | `bool`   | Prevents editing of presets when active.                                       |
