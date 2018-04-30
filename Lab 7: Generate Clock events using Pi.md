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
 
##Configure RTC on Pi
* Install the Utilities
       sudo apt-get update
       sudo apt-get install python-smbus
       sudo apt-get install i2c-tools
* Enable kernel support
       * sudo raspi-config
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

![Screenshot 2018-04-30 12.30.42.png](https://bitbucket.org/repo/BgdaKR7/images/2390713276-Screenshot%202018-04-30%2012.30.42.png)

##References
[About Adafruit DS3231 Precision RTC Breakout](https://cdn-shop.adafruit.com/product-files/3013/DS3231.pdf)
[RTC Assembly](https://learn.adafruit.com/adafruit-ds3231-precision-rtc-breakout/assembly)
[Connecting RTC to Raspberry Pi](http://www.intellamech.com/RaspberryPi-projects/rpi_RTCds3231)