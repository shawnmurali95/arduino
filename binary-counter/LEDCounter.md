#LED Binary Counter

##Requirements
###Knowledge
1. [Counting in binary](http://www.techlab.education)
2. [Basic breadboard and circuits](http://www.techlab.education)

###Hardware
1. Arduino Uno board or clone
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

The LED has two legs: one long, one short. It is important to note as the LED is a diode (LED stands for Light Emitting Diode) and is therefore unidirectional. The longer leg connects to positive voltage and the short leg connects to ground. Install your LED such that the long leg is in a row on the left side of your breadboard and the short leg is in the same row on the right side.

The LED will burn out if we connect it directly to 5v, so it must be wired in series with a resistor. Connect the ground side of the LED to ground with a 1k resistor. 

Wire pin `13` from the Arduino to the power side of the LED. When pin `13` is written `HIGH` the LED will light, and when written `LOW` the LED will power off. At this point the project should match this diagram.

![single led](https://github.com/shawnmurali95/arduino/blob/master/binary-counter/ledcircuit.png?raw=true)

Repeat these steps to wire thr`ee more LEDs to pins `10`, `11`, and `12`. At this point the project should match this diagram.

![4 leds](https://github.com/shawnmurali95/arduino/blob/master/binary-counter/4ledcircuit.png?raw=true)

## Making the Sketch
###The Basics
Every sketch should include the following code stubs: 
```c
void setup() {

}
void loop() {

}
```
The `setup()` method runs once when the program initializes and is never called again by the Arduino afterwards. The `loop()` method is then called repeatedly until the machine is powered down.

From this common skeleton, there are three different approaches to programming the binary counter. The approaches are outlined below in order of complexity.
###Approach 1: Hard-Coded Pattern
Hard-coding a pattern is conceptually the simplest way to program the binary counter. However, it is tedious to code and is not as extendable as the other methods. 
####Defining Variables
At the top of the sketch, define four constants to define the pins connected to the LEDs. Also, declare an `int` variable, which will be used as our counter.
```c
#define LED0 10
#define LED1 11
#define LED2 12
#define LED3 13

int i = 0;
```
####Defining Methods
In `void setup()`, set pins `10` through `13` to `OUTPUT`. Also begin `Serial` at a baud-rate of 9600 for debug purposes.
```c
void setup() {
	Serial.begin(9600);
	pinMode(LED0, OUTPUT);
	pinMode(LED1, OUTPUT);
	pinMode(LED2, OUTPUT);
	pinMode(LED3, OUTPUT);
}
```
Before finishing the currently empty `void loop()`, define another method `void displayPattern(int led3, int led2, int led1, int led0)`. This method will check each LED, and light it up if its corresponding `led` integer is `1`. Conditional branching will be useful here.
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
	if (led0 == 1) {
		digitalWrite(LED0, HIGH);
	} else {
		digitalWrite(LED0, LOW);
	}
}
```
Now define the `void loop()` body. Depending on the integer `i`, call `displayPattern(int led3, int led2, int led1, int led0)` on the corresponding binary representation of `i`. For example, an `i` value of `3` would yield the call `displayPattern(0,0,1,1);` (recall from the lesson on binary counting that this representation is Big Endian). Then increment `i` by one; `i` must also be reset to `0` when it reaches `16`. Finally, add a one second delay so that our counter will increment once per second. Switch-case will be useful here, but conditional branching can also be used. The switch-case method is shown below.
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
	}
	i++;
	if (i == 16) {
		i = 0;
	}
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
	pinMode(LED0, OUTPUT);
	pinMode(LED1, OUTPUT);
	pinMode(LED2, OUTPUT);
	pinMode(LED3, OUTPUT);
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
	}
	i++;
	if (i == 16) {
		i = 0;
	}
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
	if (led0 == 1) {
		digitalWrite(LED0, HIGH);
	} else {
		digitalWrite(LED0, LOW);
	}
}
```
###Approach 2: Reading from a Byte
This method takes advantage of the fact that computers store decimal numbers in binary. Using a `byte` to store the number is better in this case than using `int` because the built counter is only 4 bits. Thus, as far as this program is concerned, only the first 4 bits of the `byte` are read.
####Defining Variables
Define an `int` array `pins` to store the indexes of the pins connected to the LEDs. Also define a `byte num` to store the number being displayed.
```c
int pins[4] = {13, 12, 11, 10};
byte num = 0;
```
####Defining Methods
In `void setup()` set the mode of each pin in `pins` to `OUTPUT` using a for-loop. Also begin the `Serial` at the baud-rate `9600` for debugging purposes.
```c
void setup(){
	Serial.begin(9600);
	for (int i = 0; i < 4; i++) {
		pinMode(pins[i], OUTPUT);
	} 
}
```
The idea behind this approach is to increment `byte num` and display the first 4 bits as an LED output. Inside `void loop()` call the as-of-yet unimplemented `void displayBits()` with `num` as the argument, increment `num`, and check if `num` has exceeded 15 (the highest number we can count with 4 bits) and reset it to 0 if it has. Add a delay to see the result.
```c
void loop() {
	displayBits(num);
	num++;
	if(num>15){
		num = 0;
	}
	delay(1000);
}
```
To implement `void displayBits(byte num)` use the built in `bitRead()` method built into the Arduino library. `bitRead()` takes two arguments of type `byte` and `int`. The `byte` is the `byte` from which the bit is read and the `int` is the `int` position of the bit that is to be read. An example of its use is as follows:
```c
Serial.println(bitRead(3,1));
```
This would print on the `Serial` the value 1. $3_{10}$ is represented in binary as $0000011_2$ in a `byte`. Position 1 is the second bit from the right (think array notation).

In order to get the first 4 bits from the `byte` use `readBit()` inside a for-loop with position incrementing from 0 to 3. Use this read bit to set the corresponding LED either `HIGH` or `LOW`.
```c
void displayBits(byte num){
	for (int i = 0; i < 4; i++) {
		if (bitRead(num, i) == 1) {
			digitalWrite(pins[i], HIGH);
		} else {
			digitalWrite(pins[i], LOW);
		}
	}
}
```
Bringing this all together the sketch is as follows.
```c
int pins[4] = {13, 12, 11, 10};
byte num = 0;

void setup(){
	Serial.begin(9600);
	for (int i = 0; i < 4; i++) {
		pinMode(pins[i], OUTPUT);
	} 
}

void loop() {
	displayBits(num);
	num++;
	if(num>15){
		num = 0;
	}
	delay(1000);
}

void displayBits(byte num){
	for (int i = 0; i < 4; i++) {
		if (bitRead(num, i) == 1) {
			digitalWrite(pins[i], HIGH);
		} else {
			digitalWrite(pins[i], LOW);
		}
	}
}
```
###Approach 3: Finite State Machine
A finite state machine works by determining its next state based on its previous state, based on rules applied to state variables. In this method, the binary counter will be programmed as a state machine with 4 state variables (one for the state of each LED).
####Defining Variables
At the top of the sketch, define an array to store the pins connected to the LEDs, and another array to store the state in which the LED should be (on or off). `pins` will be an array of type `int` and	`states` will be an array of type `bool` as follows:
```c
int pins[4] = {10, 11, 12, 13};
bool states[4] = {false, false, false, false};
```
Using this syntax, the values inside the `{}` are stored in the array. The first line designates pins `10`, `11`, `12`, and `13` as pins with LEDs connected to them. The second line designates the start state of each bit as "off" ($0000_2$).
####Defining Methods
Inside `void setup()`, use a for-loop to designate each pin in `pins` as an `OUTPUT`. Also start the `Serial` to read at the baud-rate `9600`.
```c
void setup() {
	Serial.begin(9600);
	for (int i = 0; i < 4; i++) {
		pinMode(pins[i], OUTPUT);
	}
}
```	
The algorithm needs to continually display the state of the LEDs, change the state, display them again, and so on. Inside `void loop()`, write the following methods `displayState()`and`changeState()` (as of now, these are unimplemented). Add a 1-second `delay` to temporarily halt execution after each call of loop.
```c
void loop() {
	displayState();
	changeState();
	delay(1000);
}
```
Our methods `displayState()` and `changesState()` are `void` methods, which means that they do not return a value. They will called repeatedly because they are inside `void loop()`.

Below `void setup()` and `void loop()`, create the method `void displayState()`. For each state in `states`, output a `HIGH` if the state is true and a `LOW` if the state is false. A for-loop will again prove useful here.
```c
if (states[i] == true) {
	digitalWrite(pins[i], HIGH);
} else {
	digitalWrite(pins[i], LOW);
}
```
The code for change state is a little less straightforward, but follows the simple rules for counting. The algorithm checks each state sequentially.

If the state is `true`, its next state will also be `true` if any of the less significant bits are in a `false`state. Use nested for-loops to implement this part of the algorithm.
```c
void changeState() {
	for (int i = 0; i < 4; i++) {
		if (states[i] == true) {
			bool anyBitOff = false;
			for (int j = i + 1; j < 4; j++) {
				if (states[j] == false) {
					anyBitOff = true;
				}
			}
			states[i] = anyBitOff;
		}
		...
```
Look closely at some key parts. Initializing the `bool anyBitOff` to false ensures that at least one of the less-significant bits must be `false` before we set `anyBitOff` to `true`. The line `if (states[j] == false) {` sets `anyBitOff` to `true` if any less-significant bit is found to be `false`. Remember, the value of `anyBitOff` does not change from its initial `false` state unless the criteria have been met.

When the current bit is in a `false` state, its next state will be `true` if all of the less-significant bits are in a `true` state. This can again be achieved with nested for-loops.
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
				if (states[j] == false) {
					everyBitOn = false;
				}
			}
			states[i] = everyBitOn;
		}
	}
```
Again, the key parts here are the initialization of `bool everyBitOn ` and the branching conditional `if (states[j] == false) {`. This in effect mirrors the previous segment of code. The initialization of  `everyBitOn`to`true` asserts that all of the less-significant bits are `true` until one is shown to be `false`. The statement `if (states[j] == false) {` changes `everyBitOn` to false if any of the less-significant bits are `false`. Remember, the value of `everyBitOn` does not change from its initial `true` state unless the criteria have been met.

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
				if (states[j] == false) {
					everyBitOn = true;
				}
			}
			states[i] = anyBitOff;
		} else {
			bool everyBitOn = true;
			for (int j = i + 1; j < 4; j++) {
				if (states[j] == false) {
					everyBitOn = false;
				}
			}
			states[i] = everyBitOn;
		}
	}
```
