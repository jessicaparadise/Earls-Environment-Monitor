# Earls-Environment-Monitor
Real-time IoT environment monitor built with ESP32, DHT11, and OLED display. Tracks temperature and humidity with AWS cloud integration — built to monitor conditions for Earl, my cat.

![Untitled](https://github.com/user-attachments/assets/41a15d56-f4ed-4633-8569-ce84b0aa22bd)


## Phase 1

## The Hardware

**ESP32**
microcontroller with WiFi and Bluetooth built in and GPIO pins (General Purpose Input/Output) that let it talk to other components

**DHT11**
A sensor that measures temperature and humidity. It communicates by sending pulses of electricity that the ESP32 interprets as numbers.

**OLED Display**
A screen that uses protocol called **I2C** (eye-squared-C) SDA (data) and SCL (clock). The clock wire keeps both devices in sync

---

## The Wiring

**DHT11 wiring**

- `+` → 3.3V power rail (gives it electricity)
- `−` → GND rail (completes the circuit)
- `S` → GPIO 4 (sends data to ESP32)

**OLED wiring**

- `VCC` → 3.3V power rail
- `GND` → GND rail
- `SCL` → GPIO 22 (clock signal)
- `SDA` → GPIO 21 (data signal)

GPIO 21 and 22 are the ESP32's dedicated **I2C pins** — hardwired into the chip for this purpose.

---

## The Code

**Libraries**

- `DHT.h` — knows how to talk to DHT sensors
- `Wire.h` — handles I2C communication
- `Adafruit_SSD1306.h` — knows how to drive your specific OLED chip
- `Adafruit_GFX.h` — handles drawing text and graphics

**setup()**
initialize the sensor, find the OLED, and display the startup message "Earl's Room Monitor."

**loop()**
Every 3 seconds it reads temp and humidity from the DHT11, formats the numbers, and draws them on the OLED screen

**I2C Address (0x3C)**
the OLED's address is 0x3C (hexadecimal).  ran I2C scanner sketch to discover this because different manufacturers sometimes use different addresses.

---

## The Debugging

**DHT11 failed** — wires weren't making solid contact and the power wasn't connected properly. Fixed by methodically checking every single wire one at a time.

**OLED not found** —  realized the wires weren't actually crossing between the two breadboards. Fixed by physically tracing every wire and confirming row by row.

**Pin sharing conflict** — DHT11 and OLED were both trying to use the same 3V3 pin on the ESP32. Fixed by routing both through the breadboard rail so the ESP32 feeds one rail and everything draws from it.

---

## Phase 2
