#Introduction
 This breakout board helps in poor-monitoring. INA219B chip on this breakout helps to measure both the high side voltage and DC current draw over I2C with 1% precision.

##How does it work?

A precision amplifier measures the voltage across the 0.1 ohm, 1% sense resistor. Since the amplifier maximum input difference is ±320mV this means it can measure up to ±3.2 Amps. With the internal 12 bit ADC, the resolution at ±3.2A range is 0.8mA. With the internal gain set at the minimum of div8, the max current is ±400mA and the resolution is 0.1mA. Advanced hackers can remove the 0.1 ohm current sense resistor and replace it with their own to change the range (say a 0.01 ohm to measure up 32 Amps with a resolution of 8mA)

##Features

* 0.1 ohm 1% 2W current sense resistor

* Up to +26V target voltage

* Up to ±3.2A current measurement, with ±0.8mA resolution

* 0.9" x 0.8" PCB

* PCB (no header or terminal block): 1.9g


![Screenshot 2018-05-01 10.54.59.png](https://bitbucket.org/repo/BgdaKR7/images/3749407616-Screenshot%202018-05-01%2010.54.59.png)

##Schematic

![Screenshot 2018-05-06 12.29.35.png](https://bitbucket.org/repo/BgdaKR7/images/3687100833-Screenshot%202018-05-06%2012.29.35.png)

##Assembly

The board comes with all surface-mount components pre-soldered.  Additional parts can be soldered using instructions in the [link](https://learn.adafruit.com/adafruit-ina219-current-sensor-breakout/assembly).