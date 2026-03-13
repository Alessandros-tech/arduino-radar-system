# arduino-radar-system
Arduino Radar Scanner

Descrizione del Progetto

Questo progetto implementa un mini-radar a scansione utilizzando un sensore a ultrasuoni montato su un servo motore.
L’idea è riprodurre il comportamento di un radar reale: il sensore ruota da sinistra a destra, misura la distanza degli ostacoli e mostra i risultati su un LCD 16x2.

Il progetto combina:

elettronica di base

sensori di distanza

servo-motori

programmazione in C++ per Arduino

lettura dati in tempo reale su display

Componenti Utilizzati

Arduino Uno

Servo SG90

Sensore a ultrasuoni HC-SR04

LCD 16x2 (modalità 4-bit)

Potenziometro per il contrasto

LED e resistenze

Cavi jumper

Breadboard

Obiettivo

Simulare un sistema radar semplice ma funzionale, che:

Effettua una scansione angolare a 180°

Misura la distanza a ciascun step

Aggiorna l’LCD in tempo reale

(Opzionale) Esporta i dati seriali per ricostruire un grafico 2D su PC

Schema di Collegamento

I collegamenti principali sono:

Servo → Pin 6

Trigger → Pin 9

Echo → Pin 10

LCD (RS/E/D4/D5/D6/D7) → 7 / 8 / 9 / 10 / 11 / 12

Per il wiring completo vedi l'immagine sopra.

Funzionamento

Il servo ruota da 0° a 180° e ritorna.

A ogni grado effettua una misurazione tramite HC-SR04.

Il valore viene filtrato e mostrato sull’LCD.

In parallelo i dati vengono inviati sulla seriale per possibili grafici (Processing / Python).

Struttura del Repository
/images        → foto del progetto e schema
/code          → tutto il codice Arduino
/README.md     → documentazione del progetto
Miglioramenti Futuri

Visualizzazione radar in stile “sonar” su PC

Aggiunta di un buzzer per allarme distanza

Aumento precisione con filtri (media mobile / Kalman)

Integrazione con un’app o dashboard grafica

Autore

Progetto realizzato da Alessandro Valentini, 2026.
