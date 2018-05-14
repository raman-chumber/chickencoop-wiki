EEE 174 Final Combined
Components: 
12 Vdc power supply
Vdc stepper motor
Motor Breakout board
5Vdc power supply
12V DC Water Valve
NPN transistor
Dioed 
Capacitive Touch sensor
3 x 470 Ω resistor
3 x LED
L298 dual H-bridge on breakout board
12 Vdc motor

	





I ran into issues integrating every part of this lab. First, I was unable to get the LCD from lab 10 to function. The next lab I integrated was lab 8 with the touch sensors. I purchased a 4 digit touch sensor, but I could not get the pi to detect the sensor, so for the rest of the lab I used push buttons instead of touch sensors. When I wanted one of the motors or the valve to turn on, I could press the corresponding button. A LED would light up and some status text would print to the terminal. Integrating lab 7 was difficult due to water hazards. I learned how to use SSH so I could use the Pi remotely using my cell phone in the bathroom. The water valve required a 3 psi pressure to shut the valve off, and I did not have the tubing or other tools to set up a proper demonstration. The next lab I added was the motor and H-bridge, lab 9, this lab worked as expected. The last lab I tried to integrate was lab 6. I ran into major issues and I could not get the stepper motor code to work within the lab 10 code. Lab 6 worked fine on its own, but I could not get the code to work from pushing a button. 
Below is the code I wrote to try to get everything working together. Considering this is my first time working with python, I think I did okay learning some basic troubleshooting, with some time and guidance I could figure out how to get the rest of the project working. The major issues are with the logic for the button control. There is definitely a better way, a better way being just an app and not clogging up the GPIO pins with buttons and leds (The leds were 100% extra, and probably caused more problems).
	I had not planned to procure parts to make an actual chicken feeder or watering contraption, instead here all I am trying to demonstrate is that it is possible to control these processes using a python script. The base code for these projects was found on the internet, as I mentioned before, I have some basic knowledge of C and I am actively trying to learn more. I attempted to modify the scripts to add functions like turning a motor on or off with a button in another circuit. Yes, this is quite basic, but the original focus of this project was to create some food and water dispenser for chickens. The code is rough, but I will continue to learn python and linux after this project.
	
Lab 6: Stepper motor 	
Lab 7: Water valve
Lab 8: Touch sensor 
Lab 9: Bi-directional motor
Lab 10: LCD Display