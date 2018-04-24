##Introduction

In this lab we will be using 12 VDC bipolar stepper motor (angle 5.625 degrees/ 64 steps). Stepper motors can be positioned accurately, moved forward or backwards one step at a time. They are bipolar and can also rotate continuously. In this lab we will learn how to control a stepper motor using your Raspberry Pi and L298D dual H bridge driver. (Write about driver)

##Circuit Diagram



##Pin plans






##Stepper Motor coils

Stepper motors us a cogged wheel and electro magnets to nudge the wheel round a 'step' at a time. By energizing the coils in the right order, the motor is driven round. The number of steps that the stepper motor has in a 360 degree rotation is actually the number of teeth on the cog. We are using stepper motor with angle 5.625 degrees/ 64 steps. 

![Alt coils](https://cdn-learn.adafruit.com/assets/assets/000/003/696/original/learn_raspberry_pi_steppers.png?1396800693)

##Library Used

This project uses the Rpi.GPIO Library.I used GPIO connector with the breadboard for Pi. To install RPi.GPIO, we first need to install the Python Development toolkit that RPi.GPIO requires.

sudo apt-get install python-dev


Then to install Rpi.GPIO itself type:


sudo apt-get install python-rpi.gpio


You will probably be prompted to confirm by entering 'Y'.



##Reference

[GPIO Help](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-gpio)