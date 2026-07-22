---
sidebar_position: 1
---

# PIR Motion Sensor

## Introduction
PIR (Passive Infrared) motion sensors are widely used in indoor security applications. Their working principle is that the detection element converts detected infrared radiation from the human body into a weak voltage signal, which is amplified and then output. To improve detection sensitivity and increase detection distance, a plastic Fresnel lens is generally installed in front of the detector. Together with the amplification circuit, this can amplify the signal by more than 70dB, enabling detection of human movement within a range of 5–10 meters.

## Objective
Use Python programming to detect the PIR sensor module. When a person is detected, the blue indicator LED lights up (and turns off when no one is present).

## Explanation

The image below shows a commonly used PIR sensor module, which mainly has power pins and a signal output pin (the supply voltage is generally 3.3V, depending on the manufacturer's specifications).

![human_induction1](./img/human_induction/human_induction1.png)

When this module is powered on and detects a person, the sensor's signal output pin outputs a HIGH level for 3-5 seconds.

![human_induction2](./img/human_induction/human_induction2.png)

So this sensor is similar to how the button operated in the previous GPIO chapter — simply connect the module's signal pin to the WalnutPi, and the WalnutPi can detect pin level changes. The wiring between the WalnutPi and the PIR sensor is as follows:

![human_induction3](./img/human_induction/human_induction3.png)

## The digitalio Object

In CircuitPython, you can directly use the digitalio (Digital IO) module for IO programming to detect input levels. Details are as follows:

### Constructor
```python
human=digitalio.DigitalInOut(pin)
```
Parameter description:
- `pin` Board pin number. Example: board.PC8

### Methods
```python
human.direction = value
```
Define pin as input/output. Possible `value` values:
- `digitalio.Direction.INPUT` : Input.
- `digitalio.Direction.OUTPUT` : Output.

<br></br>

```python
human.pull = value
```
Set pull-up/pull-down resistor. Possible `value` values:
- `digitalio.Pull.UP` : Pull-up.
- `digitalio.Pull.DOWN` : Pull-down.

<br></br>

```python
value = human.value
```
Button input return value. Possible return values:
- `True` or `1` : HIGH.
- `False` or `0` : LOW.

<br></br>

The code writing flow is as follows:

```mermaid
graph TD
    Import digitalio-related modules --> Construct PIR and LED objects --> Detect signal input level --> HIGH lights LED, LOW turns off LED --> Detect signal input level;
```

## Reference Code

```python
'''
Experiment Name: PIR Motion Sensor
Experiment Platform: WalnutPi 1B
'''

# Import related modules
import time,board
from digitalio import DigitalInOut, Direction, Pull

# Initialize PIR sensor object, using pin PC8.
human = DigitalInOut(board.PC8) # Define pin number
human.direction = Direction.INPUT # IO as input

# Construct and initialize LED object
led = DigitalInOut(board.LED) # Define pin number
led.direction = Direction.OUTPUT  # IO as output

while True:

    if human.value == 1: # Person detected

        led.value = 1 # Turn on LED

    else: # No person detected

        led.value = 0 # Turn off LED

    time.sleep(0.5) # 0.5-second detection cycle
```

## Result

Use Thonny to remotely run the above Python code on the WalnutPi. For instructions on running Python code on the WalnutPi, please refer to: [Running Python Code](../python_run.md)

![human_induction4](./img/human_induction/human_induction4.png)

When the sensor detects a person, the blue LED lights up.

![human_induction5](./img/human_induction/human_induction5.png)

When no one is present, the blue LED turns off.

![human_induction6](./img/human_induction/human_induction6.png)

