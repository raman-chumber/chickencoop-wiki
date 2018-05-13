##Light Sensor (Digital Photo-resistor with Raspberry Pi)

#Introduction

Luminosity sensor is an advanced digital light sensor. It is a very precise sensor that allow exact lux calculations. We are using TSL2591 luminosity sensor for this lab. It can configure for different gain/timing ranges to detect light ranges from 188uLux up to 88,000 Lux on the fly. It contains both Infrared and full spectrum diodes.  

##TSL2591 luminosity sensor

![Screenshot 2018-05-01 10.19.36.png](https://bitbucket.org/repo/BgdaKR7/images/916493248-Screenshot%202018-05-01%2010.19.36.png)

##Pinouts

It uses the two I2C data/clock wires available on most micro-controllers. I2C can help sharing those pins with other sensors as long as they don't have an address collision. 

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

##Connect Raspberry Pi with digital light sensor

We used 4 wires to connect the sensor to Raspberry PI. Two of the wires used for voltage Vin (+3V from Raspberry) and ground GND and remaining two are used for data. As this is digital sensor, it uses I2C protocol to communicate with the Raspberry. For I2C we need two wires, Data (SDA) and Clock (SCL). Connect sensor SDA and SCL pins accordingly to Raspberry SDA and SCL pins.

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

##Conclusion
The sensor PCB comes with header pins and PCB separately. The pins needs to be soldered to the PCB before used. With this lab I learned soldering header pins to the PCB. Some of the documentation mentioned the sensor would work at 3.3V Vin but in my case the sensor would only work at 5V Vin. This sensor has extremely low current draw of 0.4mA while sensing and o.5 micro Ampere while in power down mode. This makes it extremely useful for battery driven applications like this Chicken Coup. The Lux sensor is very sensitive to changes in ambient lighting. This sensor will be used to sense when to open or close the coup doors based on sunrise or sunset. 

The I2C function on Raspberry PI is powerful. As you can see in the I2Cdetect screenshot, there are three different sensors connected at this time. They are addressed using the I2C interface digitally. 

##Reference

[Assembly](https://learn.adafruit.com/adafruit-tsl2591/assembly)

[Sensor to Pi](https://github.com/maxlklaxl/python-tsl2591)