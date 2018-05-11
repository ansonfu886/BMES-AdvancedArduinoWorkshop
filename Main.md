# BMES Advanced Arduino Workshop

*by Anson Fu for NTU Biomedical Engineering Society*

This workshop is based on ARDUINO IDE 1.8.5, ARDUINO UNO R3 Board and assumes basic knowledge of C++ Language and electronic protot.

***Disclaimer*** *-* *This document is only meant to serve as a reference for the attendees of the workshop. It does not cover all the concepts or implementation details discussed during the actual workshop.*

<hr>

### Workshop Details:

**When?**: Satauday, 12 May 2018. 2:00 PM - 6:00 PM.</br>
**Where?**: TR +27, The Hive, Nanyang Technological University</br>
**Who?**: NTU Biomedical Engineering Society

<hr>

## Content
### 1. Binary Counter
### 2. 7 Segment Display
### 3. Buzzer
### 4. LCD Display

## Activity 1 Binary Counter

### 1.1 Introduction to Binary
Number systems are the methods we use to represent numbers. Binary just uses two digits, 0
and 1. Binary is also known as a base-2 number system.
### 1.2 Counting In Binary
In the base-10 number system, each digit represents a value of 10x, where X is the digit
placement from the right, starting from zero and multiplying by that digit value. For example,
123 in decimal is: </br>
1×102+3×101+3×100=123. </br>
123 in binary would be: </br>
1×26+1×25+1×24+1×23+0×22+1×21+1×20=123. </br>

### 1.3 LED Binary Counter
Let's create a counter that counts in binary.
![binary1](image/binary.JPG)

```C+
int button = 2; //set to correct pin
int presses = 0;
long time = 0;
long debounce = 100;
const byte numPins = 3;
byte LEDpins[] = {3, 4, 5}; //set to correct pins
void setup() {
Serial.begin(9600);
for(int i = 0; i < numPins; i++) {
pinMode(LEDpins[i], OUTPUT);
}
pinMode(button, INPUT_PULLUP);
attachInterrupt(0, count, LOW);
}
void loop() {
String binNumber = String(presses, BIN);
int binLength = binNumber.length();
boolean led0 = binNumber.charAt(binNumber.length()-1)=='1';
boolean led1 = binNumber.charAt(binNumber.length()-2)=='1';
boolean led2 = binNumber.charAt(binNumber.length()-3)=='1';
if(presses <= 7) {
digitalWrite(LEDpins[0],led0);
digitalWrite(LEDpins[1],led1);
digitalWrite(LEDpins[2],led2);
} else {
presses = 0;
}
}
void count() {
if(millis() - time > debounce){
presses++;
}
time = millis();
}
```
![binary](image/LEDBinaryCounter.jpg)
