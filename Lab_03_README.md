# Lab Experiment 03 — I2C Based Sensor with LCD Display (BMP180)

## Student Information

| Field | Details |
|---|---|
| **Name** | Ridwan Hasan Khandakar |
| **ID** | 2310604 |
| **Section** | 03 |
| **Course Code & Title** | CSE216L — Microprocessor, Interfacing, and Assembly Language Lab |
| **Course Instructor** | Noor-E-Sadman |
| **Experiment No** | 03 |
| **Experiment Title** | Using Inter-Integrated Circuit (I2C) Based Sensor and Displaying Data on a Display |

---

## Objective

Design and simulate an Arduino Uno system that reads temperature and pressure data from a BMP180 sensor using the I2C communication protocol, and displays the values on a 16x2 I2C LCD and Serial Monitor.

---

## Circuit Diagram

> *(Circuit diagram is included in the original submission document.)*

---

## Components Used

- Arduino UNO
- BMP180 Pressure & Temperature Sensor (connected via I2C)
- 16x2 I2C LCD Display

---

## Libraries Required

- `Wire.h`
- `LiquidCrystal_I2C.h`
- `Adafruit_Sensor.h`
- `Adafruit_BMP085_U.h`

---

## Experiment Code

```cpp
/*
  This Arduino sketch reads temperature and pressure data from a BMP180 sensor
  and displays the values on a 16x2 I2C LCD. It also prints the values to the
  Serial Monitor. The BMP180 is connected via I2C, sharing the bus with the
  LCD. The Arduino UNO is used as the microcontroller.
*/

#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <Adafruit_Sensor.h>
#include <Adafruit_BMP085_U.h>

// -------- LCD Setup --------
// Change 0x27 to 0x3F if your LCD doesn't display anything
LiquidCrystal_I2C lcd(0x27, 16, 2);

// -------- BMP180 Setup --------
Adafruit_BMP085_Unified bmp = Adafruit_BMP085_Unified(10085);

void setup() {
  Serial.begin(9600);

  // Initialize LCD
  lcd.begin(16, 2);
  lcd.backlight();

  // Initialize BMP180 sensor
  if (!bmp.begin()) {
    Serial.print("Could not find a valid BMP180 sensor, check wiring!");
    while (1);
  }

  // Welcome message
  lcd.setCursor(0, 0);
  lcd.print("BMP180 Sensor");
  lcd.setCursor(0, 1);
  lcd.print("Initializing...");
  delay(2000);
  lcd.clear();
}

void loop() {
  sensors_event_t event;
  bmp.getEvent(&event);

  if (event.pressure) {
    float temperature;
    bmp.getTemperature(&temperature);

    // ---- Serial Output ----
    Serial.print("Temperature: ");
    Serial.print(temperature);
    Serial.println(" C");
    Serial.print("Pressure: ");
    Serial.print(event.pressure);
    Serial.println(" hPa");

    // ---- LCD Output ----
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Temp: ");
    lcd.print(temperature);
    lcd.print(" C");
    lcd.setCursor(0, 1);
    lcd.print("Pres: ");
    lcd.print(event.pressure);
    lcd.print(" hPa");

  } else {
    Serial.println("Sensor error!");
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Sensor Error");
  }

  delay(2000); // Wait 2 seconds
}
```

---

## Summary

An Arduino Uno system was designed and simulated to read temperature and pressure data from a BMP180 sensor using the I2C communication protocol. The Arduino processes the sensor data and displays the values on a 16x2 I2C LCD while also printing them to the Serial Monitor for debugging purposes.
