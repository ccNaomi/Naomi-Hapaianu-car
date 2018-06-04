# Naomi-Hapaianu-car
#include <LiquidCrystal.h>//Don't forget to enter this library

LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

#define pwml 20
#define l1 21
#define l2 22
#define pwmr 23
#define r1 24
#define r2 25
int durationL;
int distanceL;
int durationR;
int distanceR;
int safetyDistance;

const int trigPinL = 9;
const int echoPinL = 10;

const int trigPinR= 6;
const int echoPinR = 7;

void setup() {
  // left 
  pinMode(pwml, OUTPUT);
  pinMode(l1, OUTPUT);
  pinMode(l2, OUTPUT);
  
  digitalWrite(l1, LOW);
  digitalWrite(l2, HIGH);

  pinMode(trigPinL, OUTPUT); // Sets the trigPin as an Output
  pinMode(echoPinL, INPUT); // Sets the echoPin as an Input

  //right
  pinMode(pwmr, OUTPUT);
  pinMode(r1, OUTPUT);
  pinMode(r2, OUTPUT);
  
  digitalWrite(r1, LOW);
  digitalWrite(r2, HIGH);

  pinMode(trigPinR, OUTPUT); // Sets the trigPin as an Output
  pinMode(echoPinR, INPUT); // Sets the echoPin as an Input

  lcd.begin(16, 0);

  lcd.print((distanceL + distanceR)/2);
  Serial.begin(9600); // Starts the serial communication
}
void loop() {
  lcd.setCursor(0, 1);
  lcd.print(millis() / 1000);
   // Clears the trigPin
digitalWrite(trigPinL, LOW);
digitalWrite(trigPinR, LOW);
delayMicroseconds(2);

// Sets the trigPin on HIGH state for 10 micro seconds
digitalWrite(trigPinL, HIGH);
digitalWrite(trigPinR, HIGH);
delayMicroseconds(10);

digitalWrite(trigPinL, LOW);
digitalWrite(trigPinR, LOW);

// Reads the echoPin, returns the sound wave travel time in microseconds
durationL = pulseIn(echoPinL, HIGH);
durationR = pulseIn(echoPinR, HIGH);

// Calculating the distance
distanceL= durationL*0.034/2;
distanceR= durationR*0.034/2;
// Prints the distance on the Serial Monitor
Serial.print("Distance: ");
Serial.println((distanceL + distanceR)/2);

if((distanceL > 5) && (distanceR > 5)){
  analogWrite(pwml, 250); // Send PWM signal to L298N Enable pin
  analogWrite(pwmr, 220);
   
   digitalWrite(l1, HIGH);
   digitalWrite(l2, LOW);

    // Send PWM signal to L298N Enable pin
    
   digitalWrite(r1, HIGH);
   digitalWrite(r2, LOW);

   delay(20);

  }
  safetyDistance = distance;
if (safetyDistance <= 80){ //Enter the Distance 
  digitalWrite(buzzer, HIGH);
  digitalWrite(ledPin, HIGH);
}
else{
  digitalWrite(buzzer, LOW);
  digitalWrite(ledPin, LOW);
}

// Prints the distance on the Serial Monitor
Serial.print("Distance: ");
Serial.println(distance);
}

}
