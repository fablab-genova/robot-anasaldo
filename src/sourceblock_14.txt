 // increments/decrements a counter based on the movement of a rotary encoder and
// displays the results on an LCD in digital and bar graph form.
// rotary encoder is a 5 pin. Pins, left to right:
//   Encoder pin B - connect to D2 (interrupt 0)
//   +5 VDC
//   Encoder pin A - connect to D3 (interrupt 1)
//   NC
//   Ground
// Pin D5 is used to light up an LED connected to ground with a 1K resistor
// using PWM with brightness proportional to the encoder position.

#include <LiquidCrystal.h>
#define encoder0PinA 3
#define encoder0PinB 2
#define analogOutPin 5

LiquidCrystal lcd(13, 12, 11, 10, 9, 8, 7);
volatile unsigned int encoder0Pos = 0;
unsigned int tmp = 0;
unsigned int Aold = 0;
unsigned int Bnew = 0;

void setup() {
  pinMode(encoder0PinA, INPUT);
  pinMode(encoder0PinB, INPUT);

  lcd.begin(20, 2);
  lcd.clear();

  // encoder A on interrupt 1 (pin 3)
  attachInterrupt(1, doEncoderA, CHANGE);
  // encoder B on interrupt 0 (pin 2)
  attachInterrupt(0, doEncoderB, CHANGE);
  // set up the Serial Connection
  Serial.begin (115200);
  Serial.println("Starting");
}

void loop() {
  //if position has changed, display it on serial and bar graph
  if (tmp != encoder0Pos) {
    tmp = encoder0Pos;
    Serial.println(tmp, DEC);
    lcd.setCursor(0, 0);
    lcd.print(tmp);
    lcd.print("    ");
    lcd.setCursor(0, 1);
    //scale the range of the LCD bargraph from 0-1023 to 0-20 by dividing by 50
    for (int loopCnt = 0; loopCnt < (tmp / 50) + 1 ; loopCnt++) {
      lcd.write(1);
    }
    lcd.print("                   ");
    //scale the encorer0Pos from 0 - 1023 to the range of the PWM (0 - 255) by dividing by 4.
    analogWrite(analogOutPin, tmp / 4);
  }
}

// Interrupt on A changing state
void doEncoderA() {
  // if Bnew = Aold, increment, otherwise decrement
  Bnew^Aold ? encoder0Pos++ : encoder0Pos--;
  Aold = digitalRead(encoder0PinA);
  // check for underflow (< 0)
  if (bitRead(encoder0Pos, 15) == 1) encoder0Pos = 0;
  // check for overflow (> 1023)
  if (bitRead(encoder0Pos, 10) == 1) encoder0Pos = 1023;
  constrain(encoder0Pos, 0, 1023);
}

// Interrupt on B changing state
void doEncoderB() {
  Bnew = digitalRead(encoder0PinB);
  // if Bnew = Aold, increment, otherwise decrement
  Bnew^Aold ? encoder0Pos++ : encoder0Pos--;
  // check for underflow (< 0)
  if (bitRead(encoder0Pos, 15) == 1) encoder0Pos = 0;
  // check for overflow (> 1023)
  if (bitRead(encoder0Pos, 10) == 1) encoder0Pos = 1023;
}
