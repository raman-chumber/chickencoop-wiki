##Introduction
This lab uses a TSL2591 luminosity sensor. It is an advanced digital light sensor which is ideal for wide range of light situations. It is a very precise sensor that allow exact lux calculations and can configure for different gain/timing ranges to detect light ranges from 188uLux up to 88,000 Lux on the fly. It contains both Infrared and full spectrum diodes. We can measure infrared, full-spectrum or human-visible light separately.
![rsz_1rsz_sensors_pinouts.jpg](https://bitbucket.org/repo/BgdaKR7/images/2228077247-rsz_1rsz_sensors_pinouts.jpg)

##Pinouts
It is a I2C sensor. That means it uses the two I2C data/clock wires available on most microcontrollers and can share those pins with other sensors as long as they don't have an address collision. 
![rsz_sensors_schematic.png](https://bitbucket.org/repo/BgdaKR7/images/4079381395-rsz_sensors_schematic.png)

**Power Pins**
Vin - This is the power pin. Since the chip uses 3 VDC, we have included a voltage regulator on board that will take 3-5VDC and safely convert it down. For Raspberry Pi it uses 5VDC.

3VO - this is the 3.3V output from the voltage regulator.

GND - common ground for power and logic

**I2C Logic pins**
SCL - I2C clock pin, connect to your microcontrollers I2C clock line.

SDA - I2C data pin, connect to your microcontrollers I2C data line.

**Other Pins**
INT - this is the INTerrupt pin from the sensor.

##To connect Raspberry Pi with digital light sensor

To connect this sensor to Raspberry PI you need 4 wires. Two of the wires used for voltage Vin (+3V from Raspberry) and ground GND and remaining two are used for data. As this is digital sensor, it uses I2C protocol to communicate with the Raspberry. For I2C we need two wires, Data (SDA) and Clock (SCL). Connect sensor SDA and SCL pins accordingly to Raspberry SDA and SCL pins.

![rsz_img_5936.jpg](https://bitbucket.org/repo/BgdaKR7/images/3168928982-rsz_img_5936.jpg)


##Code


```
#!python

import tsl2591

while True:

	tsl = tsl2591.Tsl2591()  # initialize

	full, ir = tsl.get_full_luminosity() # read raw values (full spectrum and ir spectrum)

	lux = tsl.calculate_lux(full, ir)  # convert raw values to lux

	print lux, full, ir
```

Compilation done successfully.
![rsz_img_5918.jpg](https://bitbucket.org/repo/BgdaKR7/images/603732369-rsz_img_5918.jpg)

Output seen below for Lux, Full, IR.
![rsz_img_5919.jpg](https://bitbucket.org/repo/BgdaKR7/images/3784567407-rsz_img_5919.jpg)

##Reference

[Assembly](https://learn.adafruit.com/adafruit-tsl2591/assembly)

[Sensor to Pi](https://github.com/maxlklaxl/python-tsl2591)