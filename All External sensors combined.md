#Introduction
In this lab I combined all the external sensors into one circuit. 

##Components

* 6V 3.4W solar Panel

* 2x 3.7V Lithium-Polymer batteries

* MCP 73871 Solar lithium ion charger

* 10K NTC Thermistor

* INA 219 Voltage Monitor

* TSL 2591 Luminosity Sensor

* DS3231 Precision Real Time Clock breakout board


##Circuit

![Screenshot 2018-05-09 13.20.56.png](https://bitbucket.org/repo/BgdaKR7/images/3267003605-Screenshot%202018-05-09%2013.20.56.png)

6V Solar panel is connected to two lithium polymer batteries of 3.7V each using MCP 73871 solar lithium ion charger. Batteries have 10K NTC thermistor attached to them to monitor the temperature. The load port of the MCP is connected to Raspberry Pi using JST cable. It is providing power to raspberry Pi.

To monitor Power supply, INA 219 voltage monitor is used. It will display the bus current, power and shunt voltage. TSL 2591 Luminosity sensor is used as light sensor. To monitor the food and water supply events DS3231 RTC is used. It also display the temperature reading. 

##Code


```
#!python

    #!/usr/bin/env python
# -*- coding: utf-8 -*-
#
#  allsensors.py

# sensor libraries from Adafruit
#==============================

#1. light sensor
import tsl2591

#2 voltage sensor INA219
from ina219 import INA219
from ina219 import DeviceRangeError
from time import sleep

#3. real time clock DS3231  
import smbus
import os
import time

# Release RTC 3231
os.system('sudo rmmod rtc_ds1307')

# Setup RTC 3231 for temperature reading
bus = smbus.SMBus(1)
address = 0x68
CONV = 32

# constants
SHUNT_OHMS = 0.1

# Function to Read light sensor data
def readlight():
	tsl = tsl2591.Tsl2591()  # initialize
	full, ir = tsl.get_full_luminosity()  # read raw values (full spectrum and ir spectrum)
	lux = tsl.calculate_lux(full, ir)  # convert raw values to lux
	print ("Brightness: %.2f lux" % lux)
	print ("Full spectrum: %.2f" % full) 
	print ("Infrared: %.2f" % ir)
	return True

# Function to read voltage data
def readvoltage():
	ina = INA219(SHUNT_OHMS)
	ina.configure()
	
	print("Bus Voltage: %.3f V" % ina.voltage())
	try:
		print("Bus Current: %.3f mA" % ina.current())
		print("Power: %.3f mW" % ina.power())
		print("Shunt voltage: %.3f mV" % ina.shunt_voltage())
	except DeviceRangeError as e:
		# Current out of device range with specified shunt resister
		print(e)
	return True

# Force a conversion and wait until it completes
def convTemp(address):
    byte_control = bus.read_byte_data(address,0x0E)
    if byte_control&CONV == 0:
        bus.write_byte_data(address, 0x0E, byte_control|CONV)
    byte_control = bus.read_byte_data(address,0x0E)
    while byte_control&CONV != 0:
        time.sleep(1)
        byte_control = bus.read_byte_data(address,0x0E)
    return True

# Get temperature in degrees C
def getTemp(address):
    convTemp(address)
    byte_tmsb = bus.read_byte_data(address,0x11)
    byte_tlsb = bus.read_byte_data(address,0x12)
    tinteger = (byte_tmsb & 0x7f) + ((byte_tmsb & 0x80) >> 7) * -2**8
    tdecimal = (byte_tmsb >> 7) * 2**(-1) + ((byte_tmsb & 0x40) >> 6) * 2**(-2)
    return tinteger + tdecimal
# Convert and output temperature data
def readtemperature():
	Celsius = getTemp(address)
	Fahrenheit = 9.0/5.0 * Celsius + 32
	print ("Fahrenheit: %.1f *F" % Fahrenheit)
	print ("Celsius: %.1f *C" % Celsius)
	return True

# loop to call functions one by one
while True:
	readlight() 			# Call light sensor function
	readvoltage()			# Call voltage sensor 
	readtemperature()		# Call temperature sensor
	print("\n")
	sleep(0.6)
```
## Output

![Screenshot 2018-05-06 18.40.02.png](https://bitbucket.org/repo/BgdaKR7/images/2640213964-Screenshot%202018-05-06%2018.40.02.png)

##Demo

The demo of the project is shown [here](https://www.youtube.com/watch?v=XVABuwi5Eag).

##Conclusion



##Reference


https://github.com/chrisb2/pi_ina219

https://learn.adafruit.com/adding-a-real-time-clock-to-raspberry-pi/set-rtc-time

https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c

http://www.intellamech.com/RaspberryPi-projects/rpi_RTCds3231