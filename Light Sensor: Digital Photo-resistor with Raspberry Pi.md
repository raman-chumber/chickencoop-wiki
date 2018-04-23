**Introduction**
This lab uses a TSL2591 luminosity sensor. It is an advanced digital light sensor which is ideal for wide range of light situations. It is a very precise sensor that allow exact lux calculations and can configure for different gain/timing ranges to detect light ranges from 188uLux up to 88,000 Lux on the fly. It contains both Infrared and full spectrum diodes. We can measure infrared, full-spectrum or human-visible light separately.

![Alt TSL2591](https://cdn-learn.adafruit.com/assets/assets/000/017/921/original/sensors_pinouts.jpg?1405097864)

**Pinouts**
It is a I2C sensor. That means it uses the two I2C data/clock wires available on most microcontrollers and can share those pins with other sensors as long as they don't have an address collision. 

![Alt Pinouts](https://cdn-learn.adafruit.com/assets/assets/000/017/913/original/sensors_schematic.png?1405025160)