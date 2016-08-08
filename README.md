# pigpio-stepper-motor

I use 28BYJ-48 stepper motor and ULN2003 driver. I connect to 6, 13, 19, 26 pin and control over pigpio using python3 on Raspberry Pi.

## Clockwise rotation to 180 degrees. Half-step sequence (Default)

```python
import pigpio
from PigpioStepperMotor import StepperMotor

pi = pigpio.pi()
motor = StepperMotor(pi, 6, 13, 19, 26)
for i in range(2048):
  motor.doСlockwiseStep()
```



## Counterclockwise rotation to 180 degrees. Half-step sequence (Default)

```python
import pigpio
from PigpioStepperMotor import StepperMotor

pi = pigpio.pi()
motor = StepperMotor(pi, 6, 13, 19, 26)
for i in range(2048):
  motor.doСounterclockwiseStep()
```



## Clockwise rotation to 360 degrees. Full-step sequence.

```python
import pigpio
from PigpioStepperMotor import StepperMotor, fullStepSequence

pi = pigpio.pi()
motor = StepperMotor(pi, 6, 13, 19, 26, sequence = fullStepSequence)
for i in range(2048):
  motor.doСlockwiseStep()
```



## Clockwise rotation to 180 degrees. Delay = 0.05. Slooooowmoooootiiiiiooooon!

```python
import pigpio
from PigpioStepperMotor import StepperMotor

pi = pigpio.pi()
motor = StepperMotor(pi, 6, 13, 19, 26,  delayAfterStep = 0.05)
for i in range(2048):
  motor.doСlockwiseStep()
```



## Control stepper motor using keyboard left and right keys

```python
import pigpio
import curses
from PigpioStepperMotor import StepperMotor

pi = pigpio.pi()
stdscr = curses.initscr()
curses.cbreak()
curses.noecho()
stdscr.keypad(True)

try:
  motor = StepperMotor(pi, 6, 13, 19, 26)
  while True:
    symbl = stdscr.getkey()
    if symbl == "KEY_LEFT":
      motor.doСlockwiseStep()
    elif symbl == "KEY_RIGHT":
      motor.doСounterclockwiseStep()
except Exception as e:
  print(e)
finally:
  curses.endwin()
  pi.stop()
```