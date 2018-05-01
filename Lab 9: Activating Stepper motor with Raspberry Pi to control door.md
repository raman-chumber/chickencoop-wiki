##Introduction

In this lab we will be using 12 VDC bipolar stepper motor (angle 5.625 degrees/ 64 steps). Stepper motors can be positioned accurately, moved forward or backwards one step at a time. They are bipolar and can also rotate continuously. In this lab we will learn how to control a stepper motor using your Raspberry Pi and L298 dual H bridge driver. 

##L298 dual h bridge driver

The L298 Dual H-Bridge DC Motor Controller will allow you to easily and independently control two motors of up to 2A each in both directions.

![Screenshot 2018-04-30 21.24.19.png](https://bitbucket.org/repo/BgdaKR7/images/853047541-Screenshot%202018-04-30%2021.24.19.png)

Features
*  Motor supply: 7 to 24 VDC

*  Control Logic: Standard TTL Logic Level

*  Output Power: Up to 2 A each

*  Enable and Direction Control Pins

*  Heatsink for IC

*  Power-On LED indicator

*  4 Direction LED indicators

##Pin plan

![Screenshot 2018-04-30 21.40.47.png](https://bitbucket.org/repo/BgdaKR7/images/3293322929-Screenshot%202018-04-30%2021.40.47.png)

##Stepper Motor coils

Stepper motors use a cogged wheel and electro magnets to nudge the wheel round a 'step' at a time. By energizing the coils in the right order, the motor is driven round. The number of steps that the stepper motor has in a 360 degree rotation is actually the number of teeth on the cog. We are using stepper motor with angle 5.625 degrees/ 64 steps. 

![Screenshot 2018-04-30 21.16.48.png](https://bitbucket.org/repo/BgdaKR7/images/3802833717-Screenshot%202018-04-30%2021.16.48.png)

For this lab, I used 12VDC stepper motor shown in the figure below.

![Screenshot 2018-04-30 21.46.29.png](https://bitbucket.org/repo/BgdaKR7/images/1469060238-Screenshot%202018-04-30%2021.46.29.png)

I used LEDs to debug for the coils. 

![Screenshot 2018-04-30 21.44.44.png](https://bitbucket.org/repo/BgdaKR7/images/1216232935-Screenshot%202018-04-30%2021.44.44.png)


##Library Used

This project uses the Rpi.GPIO Library.I used GPIO connector with the breadboard for Pi. To install RPi.GPIO, we first need to install the Python Development toolkit that RPi.GPIO requires.


            sudo apt-get install python-dev


Then to install Rpi.GPIO itself type:


             sudo apt-get install python-rpi.gpio


Confirm by entering 'Y'.

* Configuring I2C

 I2C is a very commonly used standard designed to allow one chip to talk to another. So, since the Raspberry Pi can talk I2C we can connect it to a variety of I2C capable chips and modules.The I2C bus allows multiple devices to be connected to your Raspberry Pi, each with a unique address, that can often be set by changing jumper settings on the module. It is very useful to be able to see which devices are connected to your Pi as a way of making sure everything is working.

      sudo apt-get install -y python-smbus
      sudo apt-get install -y i2c-tools

* Installing Kernel Support 

      sudo nano /etc/modules

and add these two lines to the end of the file:

      i2c-bcm2708 
      i2c-dev

Then save the file with Control-X Y <return>

##Connection

Motor is operating on 12VDC and h bridge driver has 5 volts power supply. Connection is shown below.

(ADD CIRCUIT DIAGRAM)

![Screenshot 2018-04-30 23.02.37.png](https://bitbucket.org/repo/BgdaKR7/images/3699783758-Screenshot%202018-04-30%2023.02.37.png)

##Code

```
#!python

import RPi.GPIO as GPIO
import time
 
GPIO.setmode(GPIO.BCM)
 
enable_pin = 18
coil_A_1_pin = 4
coil_A_2_pin = 17
coil_B_1_pin = 23
coil_B_2_pin = 24
 
GPIO.setup(enable_pin, GPIO.OUT)
GPIO.setup(coil_A_1_pin, GPIO.OUT)
GPIO.setup(coil_A_2_pin, GPIO.OUT)
GPIO.setup(coil_B_1_pin, GPIO.OUT)
GPIO.setup(coil_B_2_pin, GPIO.OUT)
 
GPIO.output(enable_pin, 1)
 
def forward(delay, steps):  
  for i in range(0, steps):
    setStep(1, 0, 1, 0)
    time.sleep(delay)
    setStep(0, 1, 1, 0)
    time.sleep(delay)
    setStep(0, 1, 0, 1)
    time.sleep(delay)
    setStep(1, 0, 0, 1)
    time.sleep(delay)
 
def backwards(delay, steps):  
  for i in range(0, steps):
    setStep(1, 0, 0, 1)
    time.sleep(delay)
    setStep(0, 1, 0, 1)
    time.sleep(delay)
    setStep(0, 1, 1, 0)
    time.sleep(delay)
    setStep(1, 0, 1, 0)
    time.sleep(delay)
 
  
def setStep(w1, w2, w3, w4):
  GPIO.output(coil_A_1_pin, w1)
  GPIO.output(coil_A_2_pin, w2)
  GPIO.output(coil_B_1_pin, w3)
  GPIO.output(coil_B_2_pin, w4)
 
while True:
  delay = raw_input("Delay between steps (milliseconds)?")
  steps = raw_input("How many steps forward? ")
  forward(int(delay) / 1000.0, int(steps))
  steps = raw_input("How many steps backwards? ")
  backwards(int(delay) / 1000.0, int(steps))
```
I compiled and Executed this code and got following output.

![Screenshot 2018-04-30 22.59.05.png](https://bitbucket.org/repo/BgdaKR7/images/1260765862-Screenshot%202018-04-30%2022.59.05.png)

##Motor Working Demo

The working of the motor is shown [here](https://www.youtube.com/watch?v=TrwNAtM-FM8&feature=youtu.be).


##Conclusion



##Reference

(https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-gpio)

(https://learn.adafruit.com/adafruits-raspberry-pi-lesson-10-stepper-motors?view=all)

(http://www.instructables.com/id/Raspberry-PI-L298N-Dual-H-Bridge-DC-Motor/)

(https://www.osepp.com/electronic-modules/breakout-boards/92-osepp-motor-driver-module)