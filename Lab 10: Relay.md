# PURPOSE #
In this lab I will set up relay that will be connected to a temperature and humidity and gas sensors that will be monitoring the inside of a chicken coop.  The sensors will activate or toggle the relay when target temperature, humidity, or gas levels have been reached.  

## PROCEDURE ##

![lab10pic1.gif](https://bitbucket.org/repo/BgdaKR7/images/3999901748-lab10pic1.gif)
Figure 1. Block diagram for relay.

For lab, I connected 5 pin relay to the a Pickit Max32.  I attached LEDs to both the NO and NC pins.  I then connect a temperature/ humidity and gas sensor to the same Max32 as seen in Figure 2.  

![lab10pic2.gif](https://bitbucket.org/repo/BgdaKR7/images/102005176-lab10pic2.gif)

### CONCLUSION ###
I borrowed C code from an Arduino projects website to program the relay.  I then added parts of the temperature and gas sensors to the code.  I then added temperature, humidity, and gas limits.  If the temperature were to rise above the limit, the relay would be toggled from the normally open end to the normally closed end.  Inside the chicken coop, the normally closed end will be connected to a fan, that will hopefully help lower the coop temperature.

https://arduinobasics.blogspot.com/2014/09/relay-module.html

https://randomnerdtutorials.com/guide-for-relay-module-with-arduino/