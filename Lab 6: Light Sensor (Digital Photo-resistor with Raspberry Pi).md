##Introduction
This lab uses a TSL2591 luminosity sensor. It is an advanced digital light sensor which is ideal for wide range of light situations. It is a very precise sensor that allow exact lux calculations and can configure for different gain/timing ranges to detect light ranges from 188uLux up to 88,000 Lux on the fly. It contains both Infrared and full spectrum diodes. We can measure infrared, full-spectrum or human-visible light separately.

![Alt TSL2591](https://cdn-learn.adafruit.com/assets/assets/000/017/921/original/sensors_pinouts.jpg?1405097864)

##Pinouts
It is a I2C sensor. That means it uses the two I2C data/clock wires available on most microcontrollers and can share those pins with other sensors as long as they don't have an address collision. 

![Alt Pinouts](https://cdn-learn.adafruit.com/assets/assets/000/017/913/original/sensors_schematic.png?1405025160)

**Power Pins**
Vin - This is the power pin. Since the chip uses 3 VDC, we have included a voltage regulator on board that will take 3-5VDC and safely convert it down. For Raspberry Pi it uses 5VDC.

3VO - this is the 3.3V output from the voltage regulator.

GND - common ground for power and logic

**I2C Logic pins**
SCL - I2C clock pin, connect to your microcontrollers I2C clock line.

SDA - I2C data pin, connect to your microcontrollers I2C data line.

**Other Pins**
INT - this is the INTerrupt pin from the sensor.


**Reference**
[Assembly](https://learn.adafruit.com/adafruit-tsl2591/assembly)