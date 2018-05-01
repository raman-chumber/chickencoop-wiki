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


You will probably be prompted to confirm by entering 'Y'.



##Reference

(https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-gpio)
(https://learn.adafruit.com/adafruits-raspberry-pi-lesson-10-stepper-motors?view=all)
(http://www.instructables.com/id/Raspberry-PI-L298N-Dual-H-Bridge-DC-Motor/)
(https://www.osepp.com/electronic-modules/breakout-boards/92-osepp-motor-driver-module)