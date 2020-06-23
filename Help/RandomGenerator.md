# Random Generator

## Core level methods

### Promoted

```python
GetBinaryValue(mode, minMax)
```
Get a random zero or one.

```python
GetIntValue(mode, minMax)
```
Get an integer random value.

```python
GetRandomValue(mode, minMax, decimalPoints=8)
```
Get a floating point random value.

### Private

```python
generateRandomValue(mode, minMax)
```
Generate a random value with the given mode and range.

```python
remap(val, fromMin, fromMax, toMin, toMax)
```
Remap given vale from given range to target range. 
