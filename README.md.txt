# 🌡️ ESP32 Temperature Monitoring System with OLED & Buzzer

## 📖 Project Overview
This project implements a real-time temperature monitoring system using ESP32, DS18B20 temperature sensor, SSD1306 OLED display, and a buzzer.  
The system continuously reads temperature data, displays it on an OLED screen, and activates a buzzer when the temperature exceeds a defined threshold (20°C).

---

## 🛠️ Components Used
- ESP32 Development Board
- DS18B20 Temperature Sensor
- SSD1306 OLED Display (I2C, Address 0x3C)
- Buzzer
- 4.7kΩ Pull-up Resistor (for DS18B20)
- Jumper Wires

---

## 📚 Libraries Required
Install the following libraries using Arduino Library Manager:

- OneWire
- DallasTemperature
- Wire
- Adafruit GFX
- Adafruit SSD1306

---

## 🔌 Pin Configuration

| Component | ESP32 Pin |
|------------|------------|
| DS18B20 Data Pin | GPIO 5 |
| Buzzer | GPIO 25 |
| OLED SDA | GPIO 21 |
| OLED SCL | GPIO 22 |

---

## ⚙️ System Working

1. ESP32 initializes Serial, I2C, sensor, and OLED display.
2. Temperature data is requested from DS18B20.
3. The temperature value (in °C) is displayed on the OLED.
4. The same value is printed on the Serial Monitor.
5. If temperature exceeds 20°C, the buzzer generates an alert.

---

## 🖥️ Serial Monitor Output Example

temperature 26.50 degree C

---

## 📺 OLED Output Example

26.50 deg C

---

## 🚀 Steps to Run the Project

1. Install required libraries.
2. Connect components as per pin configuration.
3. Select ESP32 board in Arduino IDE.
4. Upload the code.
5. Open Serial Monitor with baud rate set to 115200.
6. Observe real-time temperature readings.

---

## 🔔 Alert Logic

```cpp
if(temperature > 20){
    digitalWrite(BUZZER_PIN, HIGH);
    delay(50);
    digitalWrite(BUZZER_PIN, LOW);
    delay(50);
}