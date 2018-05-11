```C+

/*Seven Segment Display Connection Arduino Pin  Seven Segment Pin        0   =>   a        1   =>   b        3   =>   c        4   =>   d        5   =>   e        6   =>   f        7   =>   g */
// Make an array to save Sev Seg pin configuration of numbers
void Display_Segment(int);

// Store all configuration value of the seven segment to the array, we have taken from the table
int digit[10][7] = {{ 0,1,1,1,1,1,1},    // Digit "0"
                    { 0,0,0,0,1,1,0},    // Digit "1"
                    { 1,0,1,1,0,1,1},    // Digit "2"
                    { 1,0,0,1,1,1,1},    // Digit "3"
                    { 1,1,0,0,1,1,0},    // Digit "4"
                    { 1,1,0,1,1,0,1},    // Digit "5"
                    { 1,1,1,1,1,0,1},    // Digit "6"
                    { 0,0,0,0,1,1,1},    // Digit "7"
                    { 1,1,1,1,1,1,1},    // Digit "8"
                    { 1,1,0,1,1,1,1 }};  // Digit "9"                                      
void setup() 
{ 
  // Seven Segment Pins as Output
  for(int a=0 ; a<=6; a++){
    pinMode(a, OUTPUT);
    }
 }

void loop() 
{  
  //Loop from 0-9 and pass it to the function
  for (int value = 0; value<=9; value++) 
  {
   delay(1000);
   Display_Segment(value); //Passing value to the function for displaying on segment
  }
  delay(2500);
}

// Function takes value and Display to the Segment
void Display_Segment(int value) 
{
  int startPin= 0;
  for (int x=6; x >= 0; x--) {  
   digitalWrite(startPin, digit[value][x]);
   startPin++; 
 }
}
```
