# Automatic Water Dispenser with Glass Detection and Water Level Monitoring

This project is an Arduino-based automatic water dispenser that uses **ultrasonic sensors** for detecting water levels in a tank and the presence of a glass to trigger a **relay-controlled pump**. An **LCD display** shows the current water level and percentage of remaining water in the tank in real-time.

## Features

- 💧 **Real-time water level measurement** using an ultrasonic sensor.
- 🥛 **Glass detection** using a separate ultrasonic sensor.
- 🔁 **Relay-based control** for activating the water pump.
- 📟 **16x2 LCD** display for tank level and status messages.
- 🔒 Automatically turns off the pump if no glass is detected.

## Hardware Components

- Arduino Uno (or compatible board)
- 2x Ultrasonic Sensors (HC-SR04)
- Relay Module (for water pump control)
- 16x2 LCD with I2C or parallel interface
- Water Pump
- Jumper wires, Breadboard, and Power Supply

## Pin Configuration

| Component                | Arduino Pin |
|-------------------------|-------------|
| Water Level Trig        | D7          |
| Water Level Echo        | D6          |
| Glass Detection Trig    | D9          |
| Glass Detection Echo    | D8          |
| Relay Control (Pump)    | D4          |
| LCD Pins (RS, E, D4–D7) | D12, D11, D5, D3, D2, D1 |

> Note: If using I2C for the LCD, update the `LiquidCrystal` initialization accordingly.

## How It Works

1. **Water Level Monitoring**  
   Measures the distance from the ultrasonic sensor to the water surface and maps it to the tank capacity to compute a percentage.

2. **Glass Detection**  
   Uses a second ultrasonic sensor to detect whether a glass is placed below the dispenser.

3. **Automatic Dispensing**  
   When a glass is detected, the pump is turned on via a relay and starts dispensing water. The water level is updated after each dispense.

4. **LCD Display**  
   Shows the current water level (in cm) and the remaining water percentage. Also displays pump status (e.g., *Dispensing Water* or *Water OK*).

## Code Overview

- `measureWaterLevel()` – Triggers the water level sensor and returns the measured distance in cm.
- In the `loop()`:
  - Water level is measured and updated.
  - LCD displays both numerical level and percentage.
  - If a glass is detected (distance < 10 cm), the pump is activated.
  - The system simulates water consumption by reducing the `currentWaterLevel` variable.

## Future Improvements

- Add a **buzzer or LED indicator** when the tank is empty.
- Display **“Tank Empty”** or **“Low Water”** on the LCD.
- Track and limit the **volume of water dispensed per glass**.
- Add **capacitive touch sensors** for more intuitive control.
- Integrate with **IoT platforms** like Blynk or ThingSpeak for remote monitoring.

## Demo
![WhatsApp Video 2025-04-09 at 16 31 49](https://github.com/user-attachments/assets/d8902d40-937f-4f33-acfc-a72fd880038a)



## License

This project is open-source and free to use under the MIT License.

