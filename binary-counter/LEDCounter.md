#LED Binary Counter
(insert video here)
##Requirements
###Knowledge
1. [Counting in binary](http://www.techlab.education)
2. [Basic breadboard and circuits](http://www.techlab.education)

###Hardware
1. Arduino
2.  Programming cable
3. 4 LEDs
4. 4 1k Ohm resistor
5. Jumper cables
6. Solder-less breadboard

###Software
1. Arduino 1.6.9 or higher


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

From this common skeleton there are three methods to program the binary counter listed in order of complexity.
###Method 1: Hard-Coded Pattern
Hard-coding a pattern is the simplest way to program the binary counter. While conceptually simple, it is tedious to code and is not as extendable as the other methods. 
####Defining Variables
At the top of the sketch define four constants to define the pins connected to the LEDs and an `int` variable to step through the pattern.
```c
#define LED0 10
#define LED1 11
#define LED2 12
#define LED3 13

int i = 0;
```
####Defining Methods
In `void setup()` set pins `10` through `13` to `OUTPUT` using a for loop. Also begin `Serial` at a baud-rate of 9600 for debug purposes.
```c
void setup() {
	Serial.begin(9600);
	pinMode(LED0,OUTPUT);
	pinMode(LED1,OUTPUT);
	pinMode(LED2,OUTPUT);
	pinMode(LED3,OUTPUT);
}
```
Before finishing the currently empty `void loop()` define another method `void displayPattern(int led3, int led2, int led1, int led0)` to light up each LED if its corresponding `led` integer is `1`. Conditional branching will be useful here.
```c
void displayPattern(int led3, int led2, int led1, int led0) {
	if (led3 == 1) {
		digitalWrite(LED3, HIGH);
	} else {
		digitalWrite(LED3, LOW);
	}
	if (led2 == 1) {
		digitalWrite(LED2, HIGH);
	} else {
		digitalWrite(LED2, LOW);
	}
	if (led1 == 1) {
		digitalWrite(LED1, HIGH);
	} else {
		digitalWrite(LED1, LOW);
	}
	if (led3 == 1) {
		digitalWrite(LED3, HIGH);
	} else {
		digitalWrite(LED3, LOW);
	}
}
```
Now define the `void loop()` body. Depending on the integer `i`, call `displayPattern(int led3, int led2, int led1, int led0)` on the corresponding binary representation of `i`. For example an `i` value of `3` would yield the call `displayPattern(0,0,1,1);` (recall from the lesson on binary counting that this representation is Big Endian). Then increment `i` by one; `i` must also be reset to `0` when it reaches `16`. Additionally, add a one second delay. Switch-case will be useful here, but conditional branching can also be used. The switch-case method is shown below.
```c
void loop() {
	switch(i) {
		case 0:
			displayPattern(0,0,0,0);
			break;
		case 1:
			displayPattern(0,0,0,1);
			break;
		case 2:
			displayPattern(0,0,1,0);
			break;
		case 3:
			displayPattern(0,0,1,1);
			break;
		case 4:
			displayPattern(0,1,0,0);
			break;
		case 5:
			displayPattern(0,1,0,1);
			break;
		case 6:
			displayPattern(0,1,1,0);
			break;
		case 7:
			displayPattern(0,1,1,1);
			break;
		case 8:
			displayPattern(1,0,0,0);
			break;
		case 9:
			displayPattern(1,0,0,1);
			break;
		case 10:
			displayPattern(1,0,1,0);
			break;
		case 11:
			displayPattern(1,0,1,1);
			break;
		case 12:
			displayPattern(1,1,0,0);
			break;
		case 13:
			displayPattern(1,1,0,1);
			break;
		case 14:
			displayPattern(1,1,1,0);
			break;
		case 15:
			displayPattern(1,1,1,1);
			break;
		case 16:
			i = 0;
			break;
	}
	i++;
	delay(1000);	
}
		

```
Here is the sketch all together.
```c
#define LED0 10
#define LED1 11
#define LED2 12
#define LED3 13

int i = 0;

void setup() {
	Serial.begin(9600);
	pinMode(LED0,OUTPUT);
	pinMode(LED1,OUTPUT);
	pinMode(LED2,OUTPUT);
	pinMode(LED3,OUTPUT);
}

void loop() {
	switch(i) {
		case 0:
			displayPattern(0,0,0,0);
			break;
		case 1:
			displayPattern(0,0,0,1);
			break;
		case 2:
			displayPattern(0,0,1,0);
			break;
		case 3:
			displayPattern(0,0,1,1);
			break;
		case 4:
			displayPattern(0,1,0,0);
			break;
		case 5:
			displayPattern(0,1,0,1);
			break;
		case 6:
			displayPattern(0,1,1,0);
			break;
		case 7:
			displayPattern(0,1,1,1);
			break;
		case 8:
			displayPattern(1,0,0,0);
			break;
		case 9:
			displayPattern(1,0,0,1);
			break;
		case 10:
			displayPattern(1,0,1,0);
			break;
		case 11:
			displayPattern(1,0,1,1);
			break;
		case 12:
			displayPattern(1,1,0,0);
			break;
		case 13:
			displayPattern(1,1,0,1);
			break;
		case 14:
			displayPattern(1,1,1,0);
			break;
		case 15:
			displayPattern(1,1,1,1);
			break;
		case 16:
			i = 0;
			break;
	}
	i++;
	delay(1000);	
}

void displayPattern(int led3, int led2, int led1, int led0) {
	if (led3 == 1) {
		digitalWrite(LED3, HIGH);
	} else {
		digitalWrite(LED3, LOW);
	}
	if (led2 == 1) {
		digitalWrite(LED2, HIGH);
	} else {
		digitalWrite(LED2, LOW);
	}
	if (led1 == 1) {
		digitalWrite(LED1, HIGH);
	} else {
		digitalWrite(LED1, LOW);
	}
	if (led3 == 1) {
		digitalWrite(LED3, HIGH);
	} else {
		digitalWrite(LED3, LOW);
	}
}
```
###Method 2: Reading from a Byte
This method takes advantage of the fact that computers store decimal numbers in binary. Using a `byte` to store the number is better in this case than using `int` because the built counter is only 4 bits. Thus, as far as this program is concerned, only the first 4 bits of the `byte` are read.
####Defining Variables
Define an `int` array `pins` to store the index of the pins connected to the LEDs. Also define a `byte nums` to store the number being displayed.
```c
int pins[4] = 
```
###Method 3: Finite State Machine
A finite state machine works by determining its next state based on its previous state based on rules applied to state variables. In this method the binary counter will be programmed as a state machine with 4 state variables (one for the state of each LED).
####Defining Variables
At the top of the sketch define an arrays to store pins connected to the LEDs and another to store the state which the LED should be in (on or off). `pins` will be an array of type `int` and	`states` will be an array of type `bool` like follows:
```c
int pins[4] = {10,11,12,13};
bool states[4] = {false,false,false,false};
```
The values inside the `{}` are stored in the array with this type of initialization. The first line designates pins `10`, `11`, `12`, and `13` as pins with LEDs on them. The second line designates the start state as all bits off (binary 0).
####Defining Methods
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
