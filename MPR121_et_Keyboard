  /*
  3X4-MPR121-Capacitive-Touch-Keypad-Module
  Modified on 10 Jan 2021
  by Amir Mohammad Shojaee @ Electropeak
  based on Adafruit Library Example 
  Modifié Makoto
*/
#include <Keyboard.h>
#include "Adafruit_MPR121.h"

// You can have up to 4 on one i2c bus but one is enough for testing!
Adafruit_MPR121 cap = Adafruit_MPR121();

/* Software Debounce Interval */
#define DEBOUNCE 10

// Keeps track of the last pins touched
// so we know when buttons are 'released'
uint16_t lasttouched = 0;
uint16_t currtouched = 0;
unsigned int buttonPin[12] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11};
unsigned long keyTimer[12] = {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0};
bool buttonState[12];
bool switchType[12] = {true, true, true, true, true, true, true, true, true, true, true, true};
char asciiKey[12] = {0x39, 0x36, 0x33, 0x63, 0x38, 0x35, 0x32, 0x64, 0x37, 0x34, 0x31, 0x30};  // 7894561230cd  en clavier US

void setup() {
  Keyboard.begin();
  Serial.begin(9600);

//  while (!Serial) { // needed to keep leonardo/micro from starting too fast!
//    delay(10);
//  }
  
  Serial.println("Adafruit MPR121 Capacitive Touch sensor test"); 
  
  // Default address is 0x5A, if tied to 3.3V its 0x5B
  // If tied to SDA its 0x5C and if SCL then 0x5D
  if (!cap.begin(0x5A)) {
    Serial.println("MPR121 not found, check wiring?");
    while (1);
  }
  Serial.println("MPR121 found!");
}

void loop() {
  checkAllKeyEvents();
//  pavenum();
//  test();
}

void test() {
    currtouched = cap.touched();
    Serial.print(currtouched); Serial.println(" touched | ");
    delay(1000);
}

void checkAllKeyEvents() {
  // Get the currently touched pads
  currtouched = cap.touched();
  
  for (int i = 0; i < 12; i++) {
    if ((currtouched & (1 << i)) && !(lasttouched & (1 << i))) {     // it if *is* touched and *wasnt* touched before, alert!
      Serial.print(i); Serial.println(" touched | ");
//    if(switchType[i] == true){
      if(buttonState[i] == false){
        Keyboard.press(asciiKey[i]);
        buttonState[i] = true;
        keyTimer[i] = millis();
        Keyboard.releaseAll();
      }
      else if(buttonState[i] == true && millis() - keyTimer[i] > DEBOUNCE){
        Keyboard.release(asciiKey[i]);
        buttonState[i] = false;
      }
//    }
//    else{
//      if(buttonState[i] == false){
//        Keyboard.press(asciiKey[i]);
//        buttonState[i] = true;
//        keyTimer[i] = millis();
//        Keyboard.releaseAll();
//      }
//      else if(buttonState[i] == true && millis() - keyTimer[i] > DEBOUNCE){
//        Keyboard.release(asciiKey[i]);
//        buttonState[i] = false;
//      }
//    }
  }
}
  // reset our state
  lasttouched = currtouched;
}
// +7894561230IX
void pavenum() {
  // Get the currently touched pads
  currtouched = cap.touched();
  
  for (uint8_t i=0; i<12; i++) {
    // it if *is* touched and *wasnt* touched before, alert!
    if ((currtouched & _BV(i)) && !(lasttouched & _BV(i)) ) {
      Serial.print(i); Serial.println(" touched | ");
      
//https://en.wikipedia.org/wiki/ASCII
      switch (i) {
        case 0:          // // ASCII pour 9 anglais, when var equals 0
          Keyboard.press(0x39);
          Keyboard.releaseAll();  
          break;
        case 1:          // // ASCII pour 6 anglais, when var equals 1
          Keyboard.press(0x36);
          Keyboard.releaseAll();  
          break;
        case 2:          // // ASCII pour 3 anglais, when var equals 2
          Keyboard.press(0x33);
          Keyboard.releaseAll();  
          break;
        case 3:
//          Keyboard.press(0x33); // rien
//          Keyboard.releaseAll();
          break;
        case 4:
          Keyboard.press(0x38); // ASCII pour 8 anglais
          Keyboard.releaseAll();
          break;
        case 5:
          Keyboard.press(0x35); // ASCII pour 5 anglais
          Keyboard.releaseAll();
          break;
        case 6:
          Keyboard.press(0x32); // ASCII pour 2 anglais
          Keyboard.releaseAll();
          break;
        case 7:
          Keyboard.press(0x30); // ASCII pour 00 anglais
          Keyboard.releaseAll();
          break;
        case 8:
          Keyboard.press(0x37); // ASCII pour 7 anglais
          Keyboard.releaseAll();
          break;
        case 9:
          Keyboard.press(0x34); // ASCII pour 4 anglais
          Keyboard.releaseAll();
          break;
         case 10:
          Keyboard.press(0x31); // ASCII pour 1 anglais
          Keyboard.releaseAll();
          break;         
        case 11:
          Keyboard.press(0x30); // ASCII pour 0 anglais
          Keyboard.releaseAll();
          break;          
        default:
          // if nothing else matches, do the default
          // default is optional
          break;
      }
    }
  }
  // reset our state
  lasttouched = currtouched;

 //delay(100);
}
