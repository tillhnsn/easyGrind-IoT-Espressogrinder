# ESP32 Grinder Controller - Mahlgrad & Grind-by-Weight

##  Projektübersicht
Ein ESP32-gesteuerter Controller zur automatischen Steuerung des Mahlgrads und des Mahlgewichts einer Espressomühle. Das System nutzt eine Wägezelle mit HX711, einen Schrittmotor zur Mahlgradverstellung und ein Webinterface zur Steuerung.

##  Features
-  **Webinterface** zur Steuerung und Konfiguration
-  **Grind-by-Weight** mit hochpräziser Wägezelle
-  **Automatische Mahlgradverstellung** mit Schrittmotor
-  **Start/Stop und Tare-Funktion** per Knopfdruck oder Webinterface
-  **Flexibel erweiterbar** durch Open-Source-Architektur

##  Benötigte Komponenten
### **Elektronische Bauteile**
- 1x **ESP32** Mikrocontroller
- 1x **HX711** Wägezellenmodul
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
- Heißklebepistole oder 3D-gedruckte Halterungen

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

##  Software Installation
1. **Arduino IDE installieren**
2. **Arduino Nano ESP32 hinzufügen**
   - **Werkzeuge → Board → Boardverwalter
3. **Benötigte Bibliotheken installieren**
4. - Oben im Code den ESP in das eigene Wlan einwählen
5. **Code hochladen**
   - Lade den Quellcode aus `/src` in die Arduino IDE.
   - Wähle den richtigen Port unter **Werkzeuge → Port**.
   - Upload starten

##  Einrichtung & Kalibrierung
1. **ESP32 starten**
2. **Mit dem Webinterface verbinden** (`http://192.168.4.1`) o.Ä.
    - IP-Adresse wird im Serial Monitor in der Arduino IDE angezeigt
4. **Waage kalibrieren**: "Tare" drücken und mit bekanntem Gewicht justieren.
5. **Testlauf**: Zielgewicht einstellen und Mahlvorgang starten.

##  Nutzung des Webinterfaces
| Funktion                  | URL                   | Parameter                | Beschreibung |
|---------------------------|------------------------|--------------------------|----------------|
| Start/Stop der Mahlung     | `/start`                | —                        | Startet oder stoppt die Mahlung |
| Waage tarieren             | `/tare`                 | —                        | Nullt die Waage |
| Zielgewicht setzen         | `/setweight`            | `?weight=<wert>`         | Setzt das gewünschte Gewicht |
| Offset setzen              | `/setoffset`            | `?offset=<wert>`         | Passt den Offset an |
| Mahlgrad anpassen          | `/setMahlgrad`          | `?grad=<stufe>`          | Stellt den Mahlgrad ein (Stufen -4 bis +4) |
| Statusdaten abrufen        | `/getData`              | —                        | Gibt JSON-Daten mit aktuellen Werten zurück |

## ⚠️ Sicherheitshinweise
- ESP32 sollte gut belüftet sein (erwärmt sich bei Betrieb).
- Der Schrittmotor kann warm werden – Temperatur überwachen.
- Isolierung aller offenen Kontakte gegen Kurzschlüsse.



##  Lizenz
Dieses Projekt steht unter der **MIT-Lizenz** und kann frei genutzt, verändert und weitergegeben werden.

---

Viel Erfolg beim Aufbau
