import RPi.GPIO as GPIO  #telling the computer that this is the raspberry pi pins
import time    # This will import and introduce the times it senses to the computer
import subprocess
# I will add these comments so that you understand it
sensor = 7   #which pin on the Pi it is
GPIO.setmode(GPIO.BOARD)       
GPIO.setup(sensor, GPIO.IN, pull_up_down=GPIO.PUD_DOWN)     #setting up the sensor for the sensing
current = GPIO.input(sensor)  # starting it's sensing
previous = current   # setting the previous to the current
def printState(current):   #defining the function printState
	#print('GPIO pin %s is %s' % (sensor, 'HIGH' if current else 'LOW')) # telling the computer to turn on or off the sensor
	print('%s' % ('ALERT' if current else ' '))
	subprocess.run(['python', 'LEDon.py'])
printState(current)   # doing the what the def is telling to do
while True:   # now is when the ship is detected part is there
	current = GPIO.input(sensor)  #naming the sensor
	if current != previous:  # doing the distancing
		printState(current)   # doing the what the def is telling to do
		previous = current
	time.sleep(0.1)
GPIO.cleanup()


