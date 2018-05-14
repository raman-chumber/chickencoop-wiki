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
		To run the stepper motor comments in blue. 	
Lab 7: Water valve
		The water valve components are in purple.
	Lab 8: Touch sensor 
	The button controls came from the touch sensor controls, these comments will be in red. The control is the same for each button so it will only be described for button 1.
Lab 9: Bi-directional motor
	This motor can turn in two directions, see comments in magenta. 

#combined.py
import time
import RPi.GPIO as GPIO GPIO.setmode(GPIO.BCM)
try:
    StepPins = [2, 3, 4, 17] # I moved this outside the other functions to try to fix it not working…
    GPIO.setup(StepPins, GPIO.OUT) # I set up the stepper pins to 2 ,3 4, and 17
    Seq = [[1, 0, 0, 0],  # I tried this sequence, this worked alone in lab 6
           [1, 1, 0, 0],
           [0, 1, 0, 0],
           [0, 1, 1, 0],
           [0, 0, 1, 0],
           [0, 0, 1, 1],
           [0, 0, 0, 1],
           [1, 0, 0, 1]]
    StepCount = len(Seq) # length of Seq is 8
    StepDir = 1 # counter
    WaitTime = 0.005 # timer
    # Initialize variables
    StepCounter = 0 # steps start at 0
    LoopCounter = 0 # start loop at 0
    loopmultiplier = 1600 #approx 1 rev # roughly estimated that this makes the motor turn 1 rev.
    TotalLoops = 2*loopmultiplier # gives approx n turns # There is information out there to figure 
    Loops = True # statement to break loop # the exact amount of times the sequence loops
    # but being exact wasn’t necessary for a chicken feeder dispenser.
    # The goal was to have the motor turn ~360° ten times.
    # set pin for touch sensor
    PadPin1=16 # input for button 1
    LedPin1=12 # output to led
    GPIO.setup(PadPin1, GPIO.IN) # setup GPIO in
    GPIO.setup(LedPin1, GPIO.OUT) # setup GPIO out
    pressed1 = False # set an initial state for the button
    
    PadPin2=7
    LedPin2=1
    GPIO.setup(PadPin2, GPIO.IN)
    GPIO.setup(LedPin2, GPIO.OUT)
    pressed2 = False
    
    PadPin3=25
    LedPin3=24
    GPIO.setup(PadPin3, GPIO.IN)
    GPIO.setup(LedPin3, GPIO.OUT)
    pressed3 = False
    
    button1=False # initial state for button 1
    button1on="stepper motor on" # some event text
    button1off="stepper motor off"
    
    button2=False  # initial state for button 2
    button2on="valve opened"  # some event text
    button2off="valve closed"
    
    button3=False  # initial state for button 3
    button3on="forward/reverse motor on"  # some event text
    button3off="forward/reverse motor off"
    
    while True:
        PadPressed1=GPIO.input(PadPin1) # set a variable for when GPIO16 has input
        PadPressed2=GPIO.input(PadPin2)
        PadPressed3=GPIO.input(PadPin3)
        
        if pressed1 and not PadPressed1: # if the button state is true but GPIO16 is not true than the button state is false
            button1=False
            print(button1off) # print a message for the button turning off
            GPIO.output(LedPin1, GPIO.LOW) # turn off led
        if PadPressed1 and not pressed1: # if GPIO16 is true and the button state is false than the button turns on. 
            button1=True # change button state to true
            print(button1on) # print a message
            GPIO.output(LedPin1, GPIO.HIGH) # turn on a LED
        pressed1=PadPressed1 # change initial state of button
        time.sleep(0.1) # wait timer
        
        if pressed2 and not PadPressed2:
            button2=False
            print(button2off)
            GPIO.output(LedPin2, GPIO.LOW)  
        if PadPressed2 and not pressed2:
            button2=True
            print(button2on)
            GPIO.output(LedPin2, GPIO.HIGH)  
        pressed2=PadPressed2
        time.sleep(0.1)
        
        if pressed3 and not PadPressed3:
            button3=True
            GPIO.output(LedPin3, GPIO.LOW)   
        if PadPressed3 and not pressed3:
            print(button3on)
            GPIO.output(LedPin3, GPIO.HIGH)    
        pressed3=PadPressed3
        time.sleep(0.1)
        
        if(button1==True): # if button 1 is pressed
            
            while(Loops): # while loop counter is true
        
                for pin in range(0,4): # range of pin : 0, 1, 2, 3
                    xpin = StepPins[pin] #Get GPIO # this came from the original code
                    
                if Seq[StepCounter][pin]!=0: # this came from the original code
                    GPIO.output(xpin, True) # this came from the original code

                else: # this came from the original code

                    GPIO.output(xpin, False)
                StepCounter += StepDir
                LoopCounter += StepDir
                # statement to stop motor
                if (LoopCounter==TotalLoops):
                    Loops = False
                # If the sequence ends
                # start again
                if (StepCounter>=StepCount): # the steps will count to 8 then start again
                    StepCounter = 0
                if (StepCounter<0): # increments step counter
                    StepCounter = StepCount+StepDir
            
                # Wait before moving on
                time.sleep(WaitTime)
        
        if(button2==True):
           ValveTime=10 # set time for valve to operate
           basepin = 26	#set pin for base
           GPIO.setup(basepin, GPIO.OUT)
           GPIO.output(basepin, GPIO.HIGH)
           time.sleep(ValveTime) # valve leave valve open for set time
           GPIO.output(basepin, GPIO.LOW)

        if(button3==True):
            forward = 20 #GPio pin 
            backward = 21 #GPio pin
            sleeptime=1 #wait timer
            ftime = 2 # time motor goes forward 
            rtime = 2  # time motor goes in reverse
            loopcount = 2 # loop counter
    
            GPIO.setup(forward, GPIO.OUT) # assign pin as output
            GPIO.setup(backward, GPIO.OUT) # assign pin as output
    
            def Forward(): #define function forward
                print("forward") # print forward
                GPIO.output(forward, GPIO.HIGH) # set pin assigned to forward high
                time.sleep(ftime) # leave pin high for some set time
                GPIO.output(forward, GPIO.LOW) # set pin low
        
            def Reverse(): # define function reverse
                print("reverse") # print reverse
                GPIO.output(backward, GPIO.HIGH) # set in assigned to reverse high
                time.sleep(rtime) # leave pin high for some set time
                GPIO.output(backward, GPIO.LOW) # set pin low
        
            for x in range(0,loopcount): # set up loop
                x += 1
                Forward() # turn motor in forward direction
                time.sleep(sleeptime) # wait
                Reverse() # turn motor in reverese direction
                time.sleep(sleeptime) # wait
            button3=False
            print(button3off)
            
except KeyboardInterrupt:
    pass
finally:
    GPIO.cleanup()