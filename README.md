# ESP32 Grinder Controller – Grind Size & Grind-by-Weight

## Project Overview
An ESP32-powered controller for automatic control of grind size and grind-by-weight in an espresso grinder.  
To avoid working with high voltage, the GBW (Grind-by-Weight) control bypasses the grinder’s start/stop button on the control panel.  
This makes the code compatible with nearly any grinder that uses a physical button for start/stop.  
The STL models for grind size adjustment need to be adapted depending on the grinder model. In this example (Baratza Sette 270), it is implemented via a clamped gear (see images).

## Features
- **Web interface** for control and configuration  
- **Grind-by-Weight**  
- **Automatic grind size adjustment** using a stepper motor  
- **Start/Stop and Tare function** via physical button or web interface  

## Required Components
### **Electronic Components**
- 1x **Arduino Nano / ESP32** microcontroller  
- 1x **HX711** load cell amplifier  
- 1x **Load cell** (up to 750g capacity)  
- 1x **Stepper motor** (e.g. 28BYJ-48)  
- 1x **ULN2003 driver board**  
- 1x **NPN transistor** (e.g. BC547)  
- 1x **Potentiometer** (10 kΩ)  
- 2x **Push buttons** (Start/Stop & Tare)  
- 1x **LED** (optional)  
- Jumper wires, connectors, breadboard  

### **Tools**
- Soldering iron and solder  
- Screwdriver  
- Multimeter for voltage testing  
- 3D-printed mounts and parts  

## Bypassing the Start/Stop Button
1. Remove the grinder control housing  
2. Measure continuity of the button using a multimeter  
3. Solder new pins onto the button’s solder joints  
4. Connect the button to the transistor collector and GND using jumper wires  

## Wiring
### **ESP32 Pin Mapping**
| Component                 | ESP32 Pin | Notes |
|---------------------------|-----------|-------|
| **HX711 DT**              | `D2`      | Data pin from load cell |
| **HX711 SCK**             | `D3`      | Clock pin from load cell |
| **LED (Status)**          | `D7`      | Indicates active grinding process |
| **Motor Control (NPN)**   | `D8`      | Used to turn motor on/off |
| **Potentiometer**         | `A0`      | Analog input for target weight |
| **Start Button**          | `D6`      | Start/Stop function |
| **Tare Button**           | `D5`      | Tares the scale |
| **Stepper Motor IN1**     | `D9`      | Control signal 1 |
| **Stepper Motor IN2**     | `D10`     | Control signal 2 |
| **Stepper Motor IN3**     | `D11`     | Control signal 3 |
| **Stepper Motor IN4**     | `D12`     | Control signal 4 |

### Transistor Configuration
| NPN Pin         | Connection |
|------------------|------------|
| **Collector**     | To grinder's bypassed start button |
| **Emitter**       | GND |
| **Base**          | Via resistor (1kΩ) to `D8` |

## Software Installation
1. **Install Arduino IDE**  
2. **Add Arduino Nano ESP32 Board**  
   - **Tools → Board → Board Manager**  
3. **Install required libraries**  
4. **Connect ESP to your Wi-Fi in the code** (change SSID and password)  
5. **Upload the code**  
   - Load source code from `Arduino Code` into the Arduino IDE  
   - Select the correct port under **Tools → Port**  
   - Start upload  

## Setup & Calibration
1. **Start the ESP32**  
2. **Connect via web interface** (e.g. `http://192.168.4.1`)  
   - The exact IP address is shown in the Arduino IDE Serial Monitor  
3. **Calibrate the scale**: press "Tare" and place a calibration weight  
   - Adjust calibration value using known weight  
   - Set value in the code under `HX711 initialization`  
   - `newValue = oldValue * (measured weight / target weight)`  
4. **Test run**: Set target weight and start grinding
5. start with offset = 0g and adjust if needed

## Grind Size Adjustment
1. If necessary, redesign 3D parts to fit your grinder  
2. **WARNING**: No endstops present → Before each use, manually set both the grinder and web interface to the finest grind setting to avoid collisions  
3. Depending on your grinder, adjust the step size in the code to get meaningful grind adjustments  

## ⚠️ Safety Notes
- Stepper motor and driver can overheat quickly  
- Isolate all open contacts to prevent short circuits  

## License
This project is licensed under the **MIT License** and may be freely used, modified, and shared.
