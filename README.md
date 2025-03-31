# ESP32 Grinder Controller - Mahlgrad & Grind-by-Weight

##  Projektübersicht
Ein ESP32-gesteuerter Controller zur automatischen Steuerung des Mahlgrads und des Mahlgewichts einer Espressomühle.
Um Arbeiten im Hochspannungsbereich zu vermeiden wird die GBW-Steuerung an den Start-Stop-Taster des Bedienfeldes überbrückt. 
Dadurch ist der Code an nahezu jeder Mühle verwendbar, welche solch einen physisches Taster besitzt.


##  Features
-  **Webinterface** zur Steuerung und Konfiguration
-  **Grind-by-Weight**
-  **Automatische Mahlgradverstellung** mit Schrittmotor
-  **Start/Stop und Tare-Funktion** per Knopfdruck oder Webinterface

##  Benötigte Komponenten
### **Elektronische Bauteile**
- 1x **ESP32** Mikrocontroller
- 1x **HX711** Load Cell Amplifier
- 1x **Wägezelle** (bis 750g Kapazität)
- 1x **Schrittmotor (z.B. 28BYJ-48)**
- 1x **ULN2003 Treiberboard**
- 1x **NPN-Transistor (z.B. BC547)**
- 1x **Potentiometer (10 kΩ)**
- 2x **Taster** (Start/Stop & Tare)
- 1x **LED** (optional)
- Jumper Kabel, Steckverbindungen, Breadboard

### **Werkzeuge**
- Lötkolben und Lötzinn
- Schraubendreher
- Multimeter zur Spannungsprüfung
- 3D-gedruckte Halterungen


##  Überbrückung des Start-Stopp-Knopf
1. Verkleidung der Steuerung demontieren
2. Durchgang des Tasters mit Multimeter messen
3. auf Lötstellen des Tasters neue Pins löten
4. mit Jumperkabel den Taster am Transistor-Kollektor und GND andchließen

##  Verkabelung
### **ESP32 Pinbelegung**
| Komponente               | ESP32 Pin  | Hinweise |
|--------------------------|-------------|------------|
| **HX711 DT**               | `D2`         | Datenpin der Waage |
| **HX711 SCK**              | `D3`         | Taktpin der Waage |
| **LED (Status)**           | `D7`         | Signalisiert aktiven Mahlvorgang |
| **Motorsteuerung (NPN)**   | `D8`         | Zum Ein-/Ausschalten des Motors |
| **Potentiometer**          | `A0`         | Analoge Eingabe für Zielgewicht |
| **Start-Taste**            | `D6`         | Start/Stop-Funktion |
| **Tare-Taste**             | `D5`         | Tarieren der Waage |
| **Schrittmotor IN1**       | `D9`         | Steuersignal 1 |
| **Schrittmotor IN2**       | `D10`        | Steuersignal 2 |
| **Schrittmotor IN3**       | `D11`        | Steuersignal 3 |
| **Schrittmotor IN4**       | `D12`        | Steuersignal 4 |

### Transistor Belegung
| NPN-PIN               | Anschluss  | 
|-----------------|-------------|
| **Kollektor**   | überbrückter Mühlentaster |
| **Emitter**     | GND |
| **Basis**       | über Vorwiderstand (1kΩ) auf `D8` |

##  Software Installation
1. **Arduino IDE installieren**
2. **Arduino Nano ESP32 hinzufügen**
   - **Werkzeuge → Board → Boardverwalter
3. **Benötigte Bibliotheken installieren**
4. -  Im Code den ESP in das eigene Wlan einwählen (SSID und Passwort anpassen)
5. **Code hochladen**
   - Lade den Quellcode aus `Arduino Code` in die Arduino IDE.
   - Wähle den richtigen Port unter **Werkzeuge → Port**.
   - Upload starten

##  Einrichtung & Kalibrierung
1. **ESP32 starten**
2. **Mit dem Webinterface verbinden** (z.B. `http://192.168.4.1`)
    - genaue IP-Adresse wird im Serial Monitor in der Arduino IDE angezeigt
4. **Waage kalibrieren**: "Tare" drücken und Waage mit Eichgewicht belasten
     - Kalibrierwert Anpassen mit Eichgewicht
     - im Code unter `HX711 Initialisierung`
     - neuerWert = alterWert*(gemessenes Gewicht / soll-Gewicht)
6. **Testlauf**: Zielgewicht einstellen und Mahlvorgang starten.


## ⚠️ Sicherheitshinweise
- ESP32 sollte gut belüftet sein (erwärmt sich bei Betrieb)
- Der Schrittmotor und sein Treiber kann schnell überhitzen
- Isolierung aller offenen Kontakte gegen Kurzschlüsse



##  Lizenz
Dieses Projekt steht unter der **MIT-Lizenz** und kann frei genutzt, verändert und weitergegeben werden.

---

Viel Erfolg beim Aufbau
