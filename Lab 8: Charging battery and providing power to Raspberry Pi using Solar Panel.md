#Introduction

In this lab we used 6V Solar Panel to charge two Lithium Ion Polymer Batteries (3.7V 1200mAh each). We can use 3.7V/4.2V lithium ion/polymer batteries. We used MCP73871 USB/DC/Solar Lithium Ion/Polymer charger-v2. We also used a 10K NTC thermistor.

## MCP73871 USB/DC/Solar Lithium Ion/Polymer charger

![390-07 2.jpg](https://bitbucket.org/repo/BgdaKR7/images/1188171953-390-07%202.jpg)

##Advantages

* 3.7V/4.2V Lithium Ion or Lithium Polymer battery charger
* Charge with 5-6V DC, USB or 6V solar panel!
* Too dark out? Use a USB mini-B cable or a 5V DC adapter
* Automatic charging current tracking for high efficiency use of any wattage solar panel
* Use any 6V solar panel (6V seems to work best, 5.5V may work, 5V does not work)
* Three color indicator LEDs - Power good, Charging and Done
* Low Battery Indicator (fixed at 3.1V) with LED output on (labeled CHRG)
* Set for 500mA max charge rate, can be adjusted from 50mA up to 1A by soldering in a resistor
* Will always draw the most current possible from a solar cell - up to the max charge rate!
* Smart load sharing automatically uses the input power when available, to keep battery from constantly charging/discharging
* Temperature monitoring of battery by soldering in a 10K NTC thermistor- suggested for outdoor projects where the battery may get hot (50°C) or cold (0°C).

##Pin Plan

![Screenshot 2018-04-30 21.07.17.png](https://bitbucket.org/repo/BgdaKR7/images/4168402367-Screenshot%202018-04-30%2021.07.17.png)

##Part1: Installing the Capacitor

The first thing to do before starting to charge with a solar panel is to install the large filtering capacitor. There is a spot on the PCB for the capacitor, I installed it directly there by soldering the wires of the capacitor into the pads as shown in the figure below.

![Screenshot 2018-04-30 15.38.01.png](https://bitbucket.org/repo/BgdaKR7/images/730971483-Screenshot%202018-04-30%2015.38.01.png)

##Part2: Solar Panel

Plug solar panel into the DC jack. Put the solar panel outside (and keep the battery out of the sun, it needs to be kept shaded!) to start charging. Once you've done that, look for the  PWR GOOD LED to indicate that the solar panel is providing power. 

![Screenshot 2018-04-30 20.41.04.png](https://bitbucket.org/repo/BgdaKR7/images/2145264248-Screenshot%202018-04-30%2020.41.04.png)

##Part3: Battery

Battery used is a 3.7 V 2000 mAh Lithium Polymer (LiPoly) battery. Plug the battery into the BATT port using a 2-pin JST cable. I used two Lithium Ion +3.7V, 1200 mAh batteries. When the CHRG charging light is lit, the battery is being charged. When the battery is full, you'll see the green DONE LED light up.

![Screenshot 2018-04-30 20.19.30.png](https://bitbucket.org/repo/BgdaKR7/images/2858985469-Screenshot%202018-04-30%2020.19.30.png)


##Part4: Temperature Monitoring

Since this part of the project will be installed outside, we needed to add temperature sensing to keep the charger from overheating the battery or attempting to charge when the battery is too hot or cold. 

![Screenshot 2018-04-30 20.43.44.png](https://bitbucket.org/repo/BgdaKR7/images/2411472449-Screenshot%202018-04-30%2020.43.44.png)

I removed the 10K surface mount resistor from the THERM pads, and solder in a 10K NTC thermistor. I attach the sensing element so it is resting between the two batteries as shown in the figure below.

![Screenshot 2018-04-30 20.47.10.png](https://bitbucket.org/repo/BgdaKR7/images/2392315685-Screenshot%202018-04-30%2020.47.10.png)

After following all the steps this is how the entire circuit looked like in working condition.

![IMG_5915.JPG](https://bitbucket.org/repo/BgdaKR7/images/3275491932-IMG_5915.JPG)

##Part5: Providing Power to Raspberry Pi

![Screenshot 2018-05-09 13.20.56.png](https://bitbucket.org/repo/BgdaKR7/images/3936752844-Screenshot%202018-05-09%2013.20.56.png)



## Conclusion

The Adafruit LI-Poly Charger used in this project is a versatile charger breakout board. This board allows connecting solar panel directly without need for soldering. The power generated from the panel can be used to charge batteries or run a load like Raspberry PI. The board handles load sharing between battery and the Raspberry PI. I could not find a JST-ph cable male - USB female cable. So I created my own cable to allow connecting a Raspberry PI to the charger board.

The solar panel needs direct sunlight and without direct light it takes long time to charge the battery. LI-Poly battery needs to be maintained at between 0 C to 40 C. If it gets too hot then it may catch fire or it could get damaged if being charged while too cold. In order to manage thermistor contact with both batteries I sandwiched the thermistor between the batteries.

In order to generate sufficient current and stable voltage for running the PI I used 2x 3.7 V batteries in parallel. This should allow the batteries to power the PI for a long time between solar charges.

The capacitor allows for a smoother transfer of power.

This charger using solar panel can power raspberry without needed any additional power or internet connectivity.




## Reference
(https://learn.adafruit.com/usb-dc-and-solar-lipoly-charger/using-the-charger?view=all#downloads)