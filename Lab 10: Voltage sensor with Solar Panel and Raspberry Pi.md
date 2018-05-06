#Introduction
This lab uses INA 219 voltage monitor breakout board that helps in power-monitoring. INA219B chip on this breakout helps to measure both the high side voltage and DC current draw over I2C with 1% precision.

##Working of INA 219 voltage monitor

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

##Raspberry Pi Python Library for Voltage Sensors Using the INA219

This library and its dependency (Adafruit GPIO library) can be installed from PyPI by executing:

                sudo pip install pi-ina219

To upgrade from a previous version installed direct from Github execute:

                sudo pip uninstall pi-ina219 
                sudo pip install pi-ina219

The Adafruit library supports the I2C protocol on all versions of the Raspberry Pi. Remember to enable the I2C bus under the Advanced Options of raspi-config.

![Screenshot 2018-05-06 12.43.35.png](https://bitbucket.org/repo/BgdaKR7/images/2795712847-Screenshot%202018-05-06%2012.43.35.png)

##Code

Simple - Auto Gain

This mode is great for getting started, as it will provide valid readings until the device current capability is exceeded for the value of the shunt resistor connected (3.2A for 0.1Ω shunt resistor). It does this by automatically adjusting the gain as required until the maximum is reached, when a DeviceRangeError exception is thrown to avoid invalid readings being taken.

The downside of this approach is reduced current and power resolution.

![Screenshot 2018-05-06 13.02.12.png](https://bitbucket.org/repo/BgdaKR7/images/424581768-Screenshot%202018-05-06%2013.02.12.png)

##Functions

* INA219() constructs the class. The arguments, are:

* shunt_ohms: The value of the shunt resistor in Ohms (mandatory).

* max_expected_amps: The maximum expected current in Amps (optional).

* address: The I2C address of the INA219, defaults to 0x40 (optional).

* configure() configures and calibrates how the INA219 will take measurements. The arguments, which are all optional, are:

* voltage_range: The full scale voltage range, this is either 16V or 32V, represented by one of the following constants (optional).

* gain: The gain, which controls the maximum range of the shunt voltage, represented by one of the following constants (optional).

* bus_adc: The bus ADC resolution (9, 10, 11, or 12-bit), or set the number of samples used when averaging results, represented by one of the following constants (optional).

* shunt_adc: The shunt ADC resolution (9, 10, 11, or 12-bit)

* voltage() Returns the bus voltage in volts (V).

* supply_voltage() Returns the bus supply voltage in volts (V). This is the sum of the bus voltage and shunt voltage. A DeviceRangeError exception is thrown if current overflow occurs.

* current() Returns the bus current in milliamps (mA). A DeviceRangeError exception is thrown if current overflow occurs.

* power() Returns the bus power consumption in milliwatts (mW). A DeviceRangeError exception is thrown if current overflow occurs.

* shunt_voltage() Returns the shunt voltage in millivolts (mV). A DeviceRangeError exception is thrown if current overflow occurs.

* current_overflow() Returns 'True' if an overflow has occured. Alternatively handle the DeviceRangeError exception as shown in the examples above.

* sleep() Put the INA219 into power down mode.

* wake() Wake the INA219 from power down mode.

* reset() Reset the INA219 to its default configuration.

##Connection

![2018-05-06-PHOTO-00000183.jpg](https://bitbucket.org/repo/BgdaKR7/images/2384691306-2018-05-06-PHOTO-00000183.jpg)

##Output

![Screenshot 2018-05-06 13.12.18.png](https://bitbucket.org/repo/BgdaKR7/images/2874891055-Screenshot%202018-05-06%2013.12.18.png)

##Conclusion









##Reference

(https://github.com/adafruit/Adafruit_INA219)

(https://github.com/chrisb2/pi_ina219)

(https://learn.adafruit.com/adafruit-ina219-current-sensor-breakout/wiring)