#LED Binary Counter
(insert video here)
##Requirements
###Knowledge
1. [Counting in binary](https://www.techlabeducation.com)
2. [Basic breadboard and circuits](http://www.techlabeducation.com)

###Hardware
1. Arduino
2.  Programming cable
3. 4 LEDs
4. 4 1k Ohm resistor
5. Jumper cables
6. Solder-less breadboard

###Software
1. Arduino 1.6.9 or higher
 
## Making the Sketch
###The Basics
Every sketch should include the following code stubs: 
```c
void setup() {
}
void loop() {
}
```
Setup runs once when the program initializes and is never called again by the Arduino. Loop is called repeatedly until the machine is powered down.
###Defining Variables
At the top of the sketch define an arrays to store pins connected to the LEDs and another to store the state which the LED should be in (on or off). `pins` will be an array of type `int` and	`states` will be an array of type `bool` like follows:
```c
int pins[4] = {10,11,12,13};
bool states[4] = {false,false,false,false};
```
The values inside the `{}` are stored in the array with this type of initialization. The first line designates pins `10`, `11`, `12`, and `13` as pins with LEDs on them. The second line designates the start state as all bits off (binary 0).
###Defining Methods
Inside `void setup()`designate each pin in `pins` as an `OUTPUT`. Use a for-loop to achieve this. Also start the `Serial` to read at the baud rate `9600`.
```c
void setup() {
	Serial.begin(9600);
	for (int i = 0; i < 4; i++) {
		pinMode(pins[i], OUTPUT);
	}
}
```	
The algorithm used needs to display the state of the LEDs, change the state, and display them again. Inside `void loop()`write the following as-of-now unimplemented methods `displayState()`and`changeState()`. Add a `delay` in milliseconds to temporarily halt execution after each call of loop.
```c
void loop() {
	displayState();
	changeState();
	delay(1000);
}
```
These two are `void` methods, those that do not return a value, and are called repeatedly because they are inside loop.

Below `void setup()` and `void loop()` create the method `void displayState()`. For each state in `states` output a `HIGH` if the state is true and a `LOW` if the state is false. For-loops will again prove useful here.
```c
void displayState() {
	for (int i = 0; i < 4; i++) {
		int output = LOW;
		if (states[i] == true) {
			output = HIGH;
		}
		digitalWrite(pins[0],output);
	}
}
```
The code for change state is a little less straightforward, but follows the simple rules for counting. The algorithm checks each state sequentially. If the state is `true` its next state depends on whether any of the less significant bits are in a `false`state. Use nested for-loops to implement this part of the algorithm.
```c
void changeState() {
	for (int i = 0; i < 4; i++) {
		if (states[i] == true) {
			bool anyBitOff = false;
			for (int j = i + 1; j < 4; j++) {
				if (anyBitOff == false){
					anyBitOff = (states[j] == false);
				}
			}
			states[i] = anyBitOff;
		}
		...
```
Look closely at some key parts. Initializing the `bool anyBitOff` to false ensures us that we prove at least one of the less-significant bits is `false` before we set `anyBitOff` to `true`. The line `if (anyBitOff == false) {` allows us to only change the value of `anyBitOff` before we have shown it to be `true`; once we have shown it to be `true` it should remain in that state for the duration of the loop.

When the bit you are checking is in a `false` state, check whether all the less-significant bits are in a `true` state. This can again be achieved with nested-for loops.
```c
void changeState() {
	for (int i = 0; i < 4; i++) {
		if (states[i] == true) {
			bool anyBitOff = false;
			for (int j = i + 1; j < 4; j++) {
				if (anyBitOff == false){
					anyBitOff = (states[j] == false);
				}
			}
			states[i] = anyBitOff;
		} else {
			bool everyBitOn = true;
			for (int j = i + 1; j < 4; j++) {
				if (everyBitOn == true) {
					everyBitOn = states[j];
				}
			}
			states[i] = everyBitOn;
		}
	}
```
Again, the key parts here are the initialization of `bool everyBitOn ` and the branching conditional `if (everyBitOn == true) {`. This in effect mirrors the previous segment of code. The assignment of  `everyBitOn`to`true` asserts that all the less-significant are `true` until one is shown to be `false`.`if (everyBitOn == true) {` only excutes the code in the block when we still have not proven any bit is `false`.

This is the full implementation of the counting algorithm in our sketch.
```c
//called once on startup
void setup() {
	Serial.begin(9600);
	for (int i = 0; i < 4; i++) {
		pinMode(pins[i], OUTPUT);
	}
}

//called repeatedly until poweroff
void loop() {
	displayState();
	changeState();
	delay(1000);
}

//turns LEDs on and off based on states
void displayState() {
	for (int i = 0; i < 4; i++) {
		int output = LOW;
		if (states[i] == true) {
			output = HIGH;
		}
		digitalWrite(pins[0],output);
	}
}

//changes states from one state to the next
void changeState() {
	for (int i = 0; i < 4; i++) {
		if (states[i] == true) {
			bool anyBitOff = false;
			for (int j = i + 1; j < 4; j++) {
				if (anyBitOff == false){
					anyBitOff = (states[j] == false);
				}
			}
			states[i] = anyBitOff;
		} else {
			bool everyBitOn = true;
			for (int j = i + 1; j < 4; j++) {
				if (everyBitOn == true) {
					everyBitOn = states[j];
				}
			}
			states[i] = everyBitOn;
		}
	}
```
Remember to wire the LEDs to the appropriate pin set up in `pins`.
##The Build
###Pin to LED
Start off by wiring a connection from `GND` to the top of the left blue rail on the breadboard. Use a jumper to connect the from the bottom of the left blue rail to the bottom of the right blue rail. This gives your board common ground.
![GND to rail](https://github.com/shawnmurali95/arduino/blob/master/binary-counter/LED1.png?raw=true)
The LED has two legs: one long, one short. It is important to note as the LED is a diode (LED stands for Light Emitting Diode) and is therefore unidirectional. The longer leg connects to positive voltage and the short leg connects to ground. Install your LED such that the long leg is in a row on the left side of your breadboard and the short leg is in the same row on the right side.
![LED in board](https://github.com/shawnmurali95/arduino/blob/master/binary-counter/LED2.png?raw=true)
The LED will burn out if we connect it directly to 5v, so we must wire a resistor in series with the LED. Connect the ground side of the LED to ground with a 1k resistor. 
![Resistor in board](https://github.com/shawnmurali95/arduino/blob/master/binary-counter/LED3.png?raw=true)
Wire pin `13` from the Arduino to the power side of the LED. When pin `13` is written `HIGH` the LED will light, and when written `LOW` the LED will power off.
![Pin to LED](https://github.com/shawnmurali95/arduino/blob/master/binary-counter/LED4.png?raw=true)
We can repeat these steps for the LEDs wired to pins `10`, `11`, and `12`. 
![Final build](https://github.com/shawnmurali95/arduino/blob/master/binary-counter/LED5.png?raw=true)
