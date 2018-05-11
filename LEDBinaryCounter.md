![binary](image/LEDBinaryCounter.jpg)

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
