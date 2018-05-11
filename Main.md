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
const byte numPins = 3; //number of pins we use
byte LEDpins[] = {3, 4, 5}; //set to correct pins

void setup() {
  Serial.begin(9600);
  for(int i = 0; i < numPins; i++) {
      pinMode(LEDpins[i], OUTPUT);
      }
  pinMode(button, INPUT_PULLUP); //monitors the state of a switch 
  attachInterrupt(0, count, LOW); //function count is triggerd when pin 0 is LOW 
  }
  
void loop() {
  String binNumber = String(presses, BIN); //give a string of binary number
  int binLength = binNumber.length(); //get the length from binary number
  boolean led0 = binNumber.charAt(binNumber.length()-1)=='1'; //search for '1' at specific location, true when '1' is found
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

## Activity 2 Seven Segment Display
If your Arduino application only needs to display numbers, consider using a seven-segment display. The severn-segment display has seven LEDs arranged in the shape of number eight. They are easy to use and cost effective. The picture below shows a typical seven-segment display.</br>
i[SSD](image/SSD.jpg)
### 2.1 Common Anode and Common Cathode
Seven segment displays are of two types: common anode and common cathode. The Internal structure of both types is nearly the same. The difference is the polarity of the LEDs and common terminal. </br>
#### 2.1.1 Common Cathode
In a common cathode seven-segment display, all seven LEDs plus a dot LED have the cathodes connected to pins 2 and pin 8. To use this display, we need to connect GROUND to pin 2 and pin 8 and,  and connect +5V to the other pins to make the individual segments light up.</br> 
![CC](image/Common_cathode.png)
#### 2.1.2 Common Anode
The common anode display is the exact opposite. In a common-anode display, the positive terminal of all the eight LEDs  are connected together and then connected to pin 3 and pin 8. To turn on an individual segment, you ground one of the pins. </br>
![CA](image/Common_cathode.png) </br>
### 2.2 Configuration
The seven segment are labelled a-g, with the dot being "dp," as shown in the figure below: </br>
![SSDnew](image/SSDnew.jpg)
To display a particular number, you turn on the individual segments as shown in the table below: </br>
![7d](image/7d.JPG)
### 2.3 Connect 7 segment display to Arduino Board
![7dAB](image/7segmentsLED.jpg)
### 2.4 Experiments
#### 2.4.1 Turn on and off
In this experiment, we will simply turn on and turn off the LEDs to get familiar with how a seven-segment display works.
```C++
void setup()
{
  // define pin modes
  
 pinMode(2,OUTPUT);
 pinMode(3,OUTPUT);
 pinMode(4,OUTPUT);
 pinMode(5,OUTPUT);
 pinMode(6,OUTPUT);
 pinMode(7,OUTPUT);
 pinMode(8,OUTPUT);
 
}

void loop() 
{
  // loop to turn leds od seven seg ON
  
  for(int i=2;i<9;i++)
  {
    digitalWrite(i,HIGH);
    delay(600);
  }
  
  // loop to turn leds od seven seg OFF
  for(int i=2;i<9;i++)
  {
    digitalWrite(i,LOW);
    delay(600);
  }
  delay(1000);
}
```
#### 2.4.2 Show numbers
In this experiment, we will turn on specific LEDs to show numbers.
```C++
#define segA 2//connecting segment A to PIN2

#define segB 3// connecting segment B to PIN3

#define segC 4// connecting segment C to PIN4

#define segD 5// connecting segment D to PIN5

#define segE 6// connecting segment E to PIN6

#define segF 7// connecting segment F to PIN7

#define segG 8// connecting segment G to PIN8

void setup() 
{
  for (int i=2;i<9;i++) {
    pinMode(i, OUTPUT);// taking all pins from 2-8 as output
    }

}

void loop()
{  // To show number 0

   digitalWrite(segA, HIGH);

   digitalWrite(segB, HIGH);

   digitalWrite(segC, HIGH);

   digitalWrite(segD, HIGH);

   digitalWrite(segE, HIGH);

   digitalWrite(segF, HIGH);

   digitalWrite(segG, LOW);
  }
```
#### 2.4.3 Count Up 
In this experiment, we will count up numbers.
```C++
#define segA 2//connecting segment A to PIN2
#define segB 3// connecting segment B to PIN3
#define segC 4// connecting segment C to PIN4
#define segD 5// connecting segment D to PIN5
#define segE 6// connecting segment E to PIN6
#define segF 7// connecting segment F to PIN7
#define segG 8// connecting segment G to PIN8

int COUNT=0;//count integer for 0-9 increment

void setup() 
{
  for (int i=2;i<9;i++) {
    pinMode(i, OUTPUT);// taking all pins from 2-8 as output
    }

}

void loop() 
{
swith(COUNT)
{ 
  case 0://when count value is zero show”0” on disp

  digitalWrite(segA, HIGH);
  digitalWrite(segB, HIGH);
  digitalWrite(segC, HIGH);
  digitalWrite(segD, HIGH);
  digitalWrite(segE, HIGH);
  digitalWrite(segF, HIGH);
  digitalWrite(segG, LOW);

  break;

  case 1:// when count value is 1 show”1” on disp

  digitalWrite(segA, LOW);
  digitalWrite(segB, HIGH);
  digitalWrite(segC, HIGH);
  digitalWrite(segD, LOW);
  digitalWrite(segE, LOW);
  digitalWrite(segF, LOW);
  digitalWrite(segG, LOW);

  break;

  case 2:// when count value is 2 show”2” on disp

  digitalWrite(segA, HIGH);
  digitalWrite(segB, HIGH);
  digitalWrite(segC, LOW);
  digitalWrite(segD, HIGH);
  digitalWrite(segE, HIGH);
  digitalWrite(segF, LOW);
  digitalWrite(segG, HIGH);

  break;

  case 3:// when count value is 3 show”3” on disp

  digitalWrite(segA, HIGH);
  digitalWrite(segB, HIGH);
  digitalWrite(segC, HIGH);
  digitalWrite(segD, HIGH);
  digitalWrite(segE, LOW);
  digitalWrite(segF, LOW);
  digitalWrite(segG, HIGH);

  break;

  case 4:// when count value is 4 show”4” on disp

  digitalWrite(segA, LOW);
  digitalWrite(segB, HIGH);
  digitalWrite(segC, HIGH);
  digitalWrite(segD, LOW);
  digitalWrite(segE, LOW);
  digitalWrite(segF, HIGH);
  digitalWrite(segG, HIGH);

  break;

  case 5:// when count value is 5 show”5” on disp

  digitalWrite(segA, HIGH);
  digitalWrite(segB, LOW);
  digitalWrite(segC, HIGH);
  digitalWrite(segD, HIGH);
  digitalWrite(segE, LOW);
  digitalWrite(segF, HIGH);
  digitalWrite(segG, HIGH);

  break;

  case 6:// when count value is 6 show”6” on disp

  digitalWrite(segA, HIGH);
  digitalWrite(segB, LOW);
  digitalWrite(segC, HIGH);
  digitalWrite(segD, HIGH);
  digitalWrite(segE, HIGH);
  digitalWrite(segF, HIGH);
  digitalWrite(segG, HIGH);

  break;

  case 7:// when count value is 7 show”7” on disp

  digitalWrite(segA, HIGH);
  digitalWrite(segB, HIGH);
  digitalWrite(segC, HIGH);
  digitalWrite(segD, LOW);
  digitalWrite(segE, LOW);
  digitalWrite(segF, LOW);
  digitalWrite(segG, LOW);

  break;

  case 8:// when count value is 8 show”8” on disp

  digitalWrite(segA, HIGH);
  digitalWrite(segB, HIGH);
  digitalWrite(segC, HIGH);
  digitalWrite(segD, HIGH);
  digitalWrite(segE, HIGH);
  digitalWrite(segF, HIGH);
  digitalWrite(segG, HIGH);

  break;

  case 9:// when count value is 9 show”9” on disp

  digitalWrite(segA, HIGH);
  digitalWrite(segB, HIGH);
  digitalWrite(segC, HIGH);
  digitalWrite(segD, HIGH);
  digitalWrite(segE, LOW);
  digitalWrite(segF, HIGH);
  digitalWrite(segG, HIGH);

  break;

  break;
}
  if (COUNT<10) {
    COUNT++;
    delay(1000);///increment count integer for every second
   }
    if (COUNT==10) {
        COUNT=0;// if count integer value is equal to 10, reset it to zero.
         delay(1000);
     }
}
```

#### 2.4.3 Count Down
In this experiment, we will count up numbers.
```C++
// make an array to save Seven Seg pin configuration of numbers

int num_array[10][7] = {  { 1,1,1,1,1,1,0 },    // 0
                          { 0,1,1,0,0,0,0 },    // 1
                          { 1,1,0,1,1,0,1 },    // 2
                          { 1,1,1,1,0,0,1 },    // 3
                          { 0,1,1,0,0,1,1 },    // 4
                          { 1,0,1,1,0,1,1 },    // 5
                          { 1,0,1,1,1,1,1 },    // 6
                          { 1,1,1,0,0,0,0 },    // 7
                          { 1,1,1,1,1,1,1 },    // 8
                          { 1,1,1,0,0,1,1 }};   // 9
                                       
//function header
void Num_Write(int);

void setup() 
{ 
  // set pin modes
  pinMode(2, OUTPUT);   
  pinMode(3, OUTPUT);
  pinMode(4, OUTPUT);
  pinMode(5, OUTPUT);
  pinMode(6, OUTPUT);
  pinMode(7, OUTPUT);
  pinMode(8, OUTPUT);
}

void loop() 
{
  
  //counter loop
  
  for (int counter = 10; counter > 0; --counter) 
  {
   delay(1000);
   Num_Write(counter-1); 
  }
  delay(3000);
}

// this functions writes values to the sev seg pins  
void Num_Write(int number) 
{
  int pin= 2;
  for (int j=0; j < 7; j++) {
   digitalWrite(pin, num_array[number][j]);
   pin++;
  }
}
```
