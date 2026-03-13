# arduino-radar-system
Arduino Radar Scanner
Overview

Questo progetto implementa un semplice radar a scansione utilizzando:

un sensore a ultrasuoni HC-SR04

un servo motore per la rotazione

un display LCD 16×2 per la visualizzazione

un microcontrollore Arduino Uno

Il sistema effettua una sweep da 0° a 180°, rileva oggetti tramite la distanza e mostra i valori sul display.
È pensato come progetto introduttivo per applicazioni simili ai sistemi radar reali: scansione, acquisizione dati, visualizzazione e movimento meccanizzato.

Funzionalità principali

Rotazione del sensore tramite servo

Misura continua della distanza

Visualizzazione dei dati su LCD

Logica di scansione a step (incrementi angolari configurabili)

Possibilità di estendere il progetto con grafici e logging dati

Hardware utilizzato

Arduino Uno

Sensore ultrasuoni HC-SR04

Servo motore SG90

Display LCD 16×2 (modalità 4 bit)

Potenziometro 10k

Cavi jumpers

Eventuale base/supporto per la struttura meccanica

Schema dei collegamenti

Inserisci qui le immagini che hai caricato:

![Setup frontale](images/setup_front.jpg)
![Setup retro](images/setup_back.jpg)
![Vista completa](images/setup_full.jpg)
Struttura del repository
/code
    main.ino
/images
    setup_front.jpg
    setup_back.jpg
    setup_full.jpg
README.md
Come funziona

Il servo ruota il sensore da 0° a 180°.

A ogni step il sensore HC-SR04 misura la distanza.

I valori vengono mostrati sull'LCD.

La scansione ricomincia dall’inizio.

Possibili estensioni

Generazione grafico radar su PC via seriale

Salvataggio dati in file CSV

Algoritmo di riconoscimento ostacoli

Visualizzazione 2D stile sonar

Servo scanning più veloce o più preciso

Licenza

Open-source — libero utilizzo per studio e prototipazione.
