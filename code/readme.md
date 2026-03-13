#include <Servo.h>
#include <LiquidCrystal.h>

// LCD (RS, E, D4, D5, D6, D7)
LiquidCrystal lcd(7, 8, 9, 10, 11, 12);

// Servo
Servo radarServo;

// Ultrasuoni (NUOVI PIN PER EVITARE CONFLITTI)
const int trigPin = 4;
const int echoPin = 5;

// LED RGB
const int ledR = A0;
const int ledG = A1;
const int ledB = A2;

long readDistance() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  long duration = pulseIn(echoPin, HIGH, 25000);
  long distance = duration * 0.034 / 2;

  if (distance == 0 || distance > 400) return 400;
  return distance;
}

void setLED(long dist) {
  if (dist < 20) {       
    digitalWrite(ledR, HIGH);
    digitalWrite(ledG, LOW);
    digitalWrite(ledB, LOW);
  } 
  else if (dist < 60) {  
    digitalWrite(ledR, HIGH);
    digitalWrite(ledG, HIGH);
    digitalWrite(ledB, LOW);
  } 
  else {                 
    digitalWrite(ledR, LOW);
    digitalWrite(ledG, HIGH);
    digitalWrite(ledB, LOW);
  }
}

void setup() {
  lcd.begin(16,2);
  lcd.print(" Radar Online ");

  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);

  pinMode(ledR, OUTPUT);
  pinMode(ledG, OUTPUT);
  pinMode(ledB, OUTPUT);

  radarServo.attach(3);

  delay(1000);
}

void loop() {
  for(int angle = 0; angle <= 180; angle += 2) {

    radarServo.write(angle);
    delay(20);

    long dist = readDistance();
    setLED(dist);

    lcd.clear();
    lcd.setCursor(0,0);
    lcd.print("Angolo: ");
    lcd.print(angle);

    lcd.setCursor(0,1);
    lcd.print("Dist: ");
    lcd.print(dist);
    lcd.print(" cm");

    delay(40);
  }

  for(int angle = 180; angle >= 0; angle -= 2) {

    radarServo.write(angle);
    delay(20);

    long dist = readDistance();
    setLED(dist);

    lcd.clear();
    lcd.setCursor(0,0);
    lcd.print("Angolo: ");
    lcd.print(angle);

    lcd.setCursor(0,1);
    lcd.print("Dist: ");
    lcd.print(dist);
    lcd.print(" cm");

    delay(40);
  }
}
