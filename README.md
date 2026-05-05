# ESP32-S3 Reproductor d'Àudio AAC des de Memòria (PROGMEM)

Aquest repositori conté un codi per a l'ESP32-S3 (escrit en C++ per a l'entorn Arduino/PlatformIO) que reprodueix un fitxer d'àudio AAC emmagatzemat directament a la memòria flaix del microcontrolador (PROGMEM) i l'envia a un amplificador d'àudio I2S (com el MAX98357A).

## 📝 Descripció del Projecte

El programa utilitza la popular llibreria d'àudio per decodificar i reproduir l'arxiu. A diferència d'altres projectes que llegeixen de targetes SD o via WiFi, aquest codi llegeix les dades musicals des d'un array de bytes definit en un fitxer d'encapçalament local (`sampleaac.h`). Això és ideal per a sons curts, alertes o missatges de veu que han d'estar sempre disponibles sense necessitat de maquinari d'emmagatzematge extern.

## 🛠 Hardware Requerit

*   Placa de desenvolupament **ESP32-S3**.
*   Amplificador/Decodificador I2S (ex: MAX98357A, UDA1334A).
*   Altaveu compatible amb l'amplificador.
*   Cables de connexió.

## 📚 Dependències i Llibreries

Aquest codi requereix la instal·lació d'una llibreria externa per funcionar. Has d'instal·lar la següent llibreria des del Gestor de Llibreries d'Arduino IDE o afegir-la al teu fitxer `platformio.ini`:

*   **ESP8266Audio** per *earlephilhower* (Malgrat el nom, és totalment compatible amb ESP32 i ESP32-S3).

## 🔌 Esquema de Connexions (Pinout)

Les connexions definides per defecte per a l'ESP32-S3 en el codi són les següents:

### Amplificador I2S (Sortida d'àudio)
| Pin I2S | ESP32-S3 GPIO | Descripció |
| :--- | :--- | :--- |
| **BCLK** | GPIO 1 | Bit Clock (Rellotge de dades) |
| **LRC** / **WS** | GPIO 2 | Left/Right Clock (Selecció de paraula) |
| **DIN** / **DOUT** | GPIO 4 | Data Input a l'amplificador (Sortida ESP32) |
| **VIN** | 5V o 3.3V | Alimentació (segons el teu mòdul) |
| **GND** | GND | Terra |

## 🚀 Instal·lació i Ús

1.  Obre l'Arduino IDE o PlatformIO.
2.  Instal·la la llibreria **ESP8266Audio**.
3.  Crea un fitxer anomenat `sampleaac.h` a la mateixa carpeta del teu projecte. Aquest fitxer ha de contenir el teu àudio convertit a un array de bytes en C. Hauria de tenir una estructura similar a aquesta:
    ```c
    const unsigned char sampleaac[] PROGMEM = {
      0xff, 0xf1, 0x50, 0x80, 0x01, 0x1f, 0xfc, ...
    };
