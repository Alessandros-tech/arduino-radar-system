# arduino-radar-system
Low-cost ultrasonic scanning radar with LCD, servo control, data visualization and real-time plotting.
🛰️ Arduino Ultrasonic Scanning Radar

Progetto di radar a ultrasuoni con servo motore, LCD e visualizzazione in tempo reale.
Sistemino completo per mappare l’ambiente da 0° a 180° tramite sensore HC-SR04 rotante.

📸 Foto del progetto
Montaggio su breadboard

Sensore + servo

Panoramica sistema

(Sostituisci i nomi delle foto con quelli presenti nella tua cartella images/.)

📌 Descrizione del progetto

Questo progetto realizza un semplice radar rotante utilizzando un sensore a ultrasuoni montato su un servo motore.
Il sistema esegue una scansione da 0° a 180°, misura la distanza con l’HC-SR04 e:

mostra angolo + distanza su LCD

accende un LED RGB in base alla distanza

invia dati (angolo, distanza) via seriale per plotting

può essere visualizzato come radar grafico tramite Processing

Il progetto replica il comportamento di un radar reale, ma con componenti low–cost.

🧰 Componenti usati

Arduino Uno

HC-SR04 (sensore ultrasuoni)

Servo SG90

LCD 16×2 (4-bit mode)

Potenziometro 10k

LED RGB + resistenze 220Ω

Breadboard

Cavi jumper

🔧 Collegamenti elettrici
Servo

GND → GND

VCC → 5V

Signal → D3

HC-SR04

Trig → D4

Echo → D5

VCC → 5V

GND → GND

LCD 16x2 (4-bit mode)

RS → D7

E → D8

D4 → D9

D5 → D10

D6 → D11

D7 → D12

RW → GND

V0 → centrale potenziometro

VCC → 5V

GND → GND

LED RGB

R → A0 (220Ω)

G → A1 (220Ω)

B → A2 (220Ω)

📟 Codice Arduino

Crea nella cartella /code/ il file: radar.ino
E incolla:

#include <LiquidCrystal.h>
#include <Servo.h>

LiquidCrystal lcd(7, 8, 9, 10, 11, 12);
Servo servoMotor;

const int trigPin = 4;
const int echoPin = 5;

const int redPin = A0;
const int greenPin = A1;
const int bluePin = A2;

long getDistance() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  long duration = pulseIn(echoPin, HIGH);
  long distance = duration * 0.034 / 2;
  return distance;
}

void setColor(int r, int g, int b) {
  analogWrite(redPin, r);
  analogWrite(greenPin, g);
  analogWrite(bluePin, b);
}

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);

  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);

  servoMotor.attach(3);
  lcd.begin(16, 2);
  lcd.print("Ultrasonic Radar");
  delay(1000);
}

void loop() {
  for (int angle = 0; angle <= 180; angle++) {
    servoMotor.write(angle);
    delay(20);

    long distance = getDistance();
    
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Ang: ");
    lcd.print(angle);
    lcd.print(" deg");

    lcd.setCursor(0, 1);
    lcd.print("Dist: ");
    lcd.print(distance);
    lcd.print(" cm");

    // LED RGB
    if (distance < 20) setColor(255, 0, 0);
    else if (distance < 50) setColor(0, 255, 0);
    else setColor(0, 0, 255);

    // Serial output for plotting
    Serial.print(angle);
    Serial.print(",");
    Serial.println(distance);
  }

  for (int angle = 180; angle >= 0; angle--) {
    servoMotor.write(angle);
    delay(20);

    long distance = getDistance();
    
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Ang: ");
    lcd.print(angle);
    lcd.print(" deg");

    lcd.setCursor(0, 1);
    lcd.print("Dist: ");
    lcd.print(distance);
    lcd.print(" cm");

    if (distance < 20) setColor(255, 0, 0);
    else if (distance < 50) setColor(0, 255, 0);
    else setColor(0, 0, 255);

    Serial.print(angle);
    Serial.print(",");
    Serial.println(distance);
  }
}
📡 Visualizzazione Radar (opzionale)

Nella cartella /processing/ puoi aggiungere uno sketch Processing che visualizza il radar in tempo reale.
Se vuoi te lo preparo io.

📝 Spiegazione tecnica

(Questa parte è importantissima per un recruiter.)

Il sistema utilizza:

ultrasuoni per misurare la distanza

servo motore per ottenere coordinate polari

LCD per visualizzare localmente i dati

seriale per inviare i dati ad un computer

LED RGB per feedback immediato

L’idea chiave è la scansione angolare:
L’angolo del servo + la distanza misurata = un punto nello spazio polare.
Ripetendo da 0° a 180° si crea una mappa dell’ambiente.

🧭 Possibili miglioramenti

sostituire HC-SR04 con TOF (VL53L0X) → più preciso

aggiungere salvataggio dati CSV

usare ESP32 e inviare i dati via WiFi

radar Doppler 5.8GHz (progetto avanzato)

👤 Autore

Alessandro Valentini
Electronics Engineering – Embedded Systems & Radar
