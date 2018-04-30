**Introduction**
The Real Time Clock maintains seconds, minutes, hours, day, date, month, and year information. For this lab we are using Adafruit DS3231 Precision RTC Breakout. It is an Extremely Accurate I²C-Integrated RTC/TCXO/Crystal. The date at the end of the month is automatically adjusted for months with fewer than 31 days, including corrections for leap year. The clock operates in either the 24-hour or 12-hour format with an AM/PM indicator. Two programmable time-of-day alarms and a programmable square-wave output are provided. Address and data are transferred serially through an I2C bidirectional bus.
A precision temperature-compensated voltage reference and comparator circuit monitors the status of VCC to
detect power failures, to provide a reset output, and to automatically switch to the backup supply when necessary. Additionally, the RST pin is monitored as a pushbutton input for generating a μP reset.


![components_3013_kit_ORIG 2.jpg](https://bitbucket.org/repo/BgdaKR7/images/919966187-components_3013_kit_ORIG%202.jpg)

## Benefits and Features
* Highly Accurate RTC Completely Manages All Timekeeping Functions
*  Accuracy ±2ppm from 0°C to +40°C
* Accuracy ±3.5ppm from -40°C to +85°C
* Digital Temp Sensor Output: ±3°C Accuracy
* Register for Aging Trim
* RST Output/Pushbutton Reset Debounce Input
* Two Time-of-Day Alarms
* Programmable Square-Wave Output Signal
* Simple Serial Interface Connects to Most Microcontrollers
* Fast (400kHz) I2C Interface
* Battery-Backup Input for Continuous Timekeeping
* Low Power Operation Extends Battery-Backup Run Time
* 3.3V Operation
* Operating Temperature Ranges: Commercial (0°C to +70°C) and Industrial (-40°C to +85°C)
* Underwriters Laboratories® (UL) Recognized

##Schematics

![Screenshot 2018-04-30 11.59.56.png](https://bitbucket.org/repo/BgdaKR7/images/1697195301-Screenshot%202018-04-30%2011.59.56.png)

##Typical Operating Circuit
![Screenshot 2018-04-30 12.09.55.png](https://bitbucket.org/repo/BgdaKR7/images/1266828269-Screenshot%202018-04-30%2012.09.55.png)

##Pin Configuration
![Screenshot 2018-04-30 12.12.42.png](https://bitbucket.org/repo/BgdaKR7/images/1255289002-Screenshot%202018-04-30%2012.12.42.png)

## Pi GPIO Pinouts with RTC
![Screenshot 2018-04-30 12.19.05.png](https://bitbucket.org/repo/BgdaKR7/images/3162830509-Screenshot%202018-04-30%2012.19.05.png)

##Part1: Configuring I2C
Follow [this link](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c
) to configure I2C on the Pi
 


##Part2: Configure RTC on Pi
* Install the Utilities
       
       sudo apt-get update
       sudo apt-get install python-smbus
       sudo apt-get install i2c-tools

* Enable kernel support
       
       sudo raspi-config

       * Choose Advanced Options then I2C and select yes to enable the interface.

* Edit the module file

        sudo nano /etc/modules

        * Add the following to the to the end of this file

                i2c-bcm2708
                i2c-dev
                rtc-ds1307

* Test the bus

Check your I2C bus with, sudo i2cdetect -y 1

After following all the steps, I got the Following output
![Screenshot 2018-04-30 12.28.43.png](https://bitbucket.org/repo/BgdaKR7/images/148155558-Screenshot%202018-04-30%2012.28.43.png)

Set date and time
When connected to the Internet, the pi automatically gets the date and time from time servers. These are quite accurate. With the command hwclock -s in rc.local, we have set the pi to override this time to match the RTC. This is fine once we have the correct time on the RTC. So let's set it to the correct time.

             sudo nptd -g -q - set the pi's system time to Internet time
             date - check the system time
             sudo hwclock -r - check the date and time of the RTC
             sudo hwclock -w - write the system time to the RTC
             sudo hwclock -s - set the system time from the RTC

Running all these commands in terminal I got the following output.

![Screenshot 2018-04-30 12.30.42.png](https://bitbucket.org/repo/BgdaKR7/images/2390713276-Screenshot%202018-04-30%2012.30.42.png)

##Part3: Converting and reading the temperature
The DS3231M has an operating temperature range of -45 C to 85 C. The RTC stores its temperature data in two registers. The upper 8 bits, representing an integer, are stored in two's complement form in register 11h. The lower 2 bits, representing the fractional portion, are in register 12h.

The RTC automatically converts the temperature (updates the registers) every 64s. The maximum allowed by the chip is once every second. A convert may be forced by setting the CONV bit of the Control register (0Eh) to 1. Once the convert is completed, the CONV is set to 0 and the temperature may be read.

The following python code is used to convert, read, and display the temperature.


```
#!python


import smbus
import os

# Release RTC 3231
os.system('sudo rmmod rtc_ds1307')

# Setup RTC 3231 for temperature reading
bus = smbus.SMBus(1)
address = 0x68
CONV = 32

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

Celsius = getTemp(address)
Fahrenheit = 9.0/5.0 * Celsius + 32
print Fahrenheit, "*F /", Celsius, "*C"
```


##Conclusion
Your pi now as a battery backed, accurate RTC installed and working. This allows quality data-logging and other applications. Additionally, the temperature data from the RTC is available for your use. In Basic GPIO on the Raspberry Pi, temperature data is used to light LEDs and send alerts.


##References
[About Adafruit DS3231 Precision RTC Breakout](https://cdn-shop.adafruit.com/product-files/3013/DS3231.pdf)
[RTC Assembly](https://learn.adafruit.com/adafruit-ds3231-precision-rtc-breakout/assembly)
[Connecting RTC to Raspberry Pi](http://www.intellamech.com/RaspberryPi-projects/rpi_RTCds3231)