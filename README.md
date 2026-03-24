Earl's Environment Monitor<br>
A real-time IoT environmental monitoring system built with an ESP32 microcontroller and AWS cloud infrastructure. Tracks temperature and humidity conditions in my cat Earl's room, with live OLED display, cloud data storage, and automated email alerts.

 Phase 1 — Hardware + OLED display<br>
 Phase 2 — AWS IoT Core MQTT connection<br>
 Phase 3 — DynamoDB storage<br>
 Phase 4 — SNS email alerts<br>
 Phase 5 — REST API + web dashboard

```
Architecture

DHT11 Sensor → ESP32 → WiFi → AWS IoT Core
                 ↓                    ↓
            OLED Display           IoT Rule
                                     ↓
                                   Lambda
                                   ↓    ↓
                              DynamoDB   SNS
                                          ↓
                                     Email Alert
```
Hardware<br>
ELEGOO ESP32<br>
DHT11<br>
SSD1306 OLED<br>
Breadboard

Wiring:<br>
DHT11 S → ESP32 GPIO4<br>
DHT11 + → 3.3V rail<br>
DHT11 − → GND rail<br>
OLED SDA → ESP32 GPIO21<br>
OLED SCL → ESP32 GPIO22<br>
OLED VCC → 3.3V rail<br>
OLED GND → GND rail<br>
![Untitled](https://github.com/user-attachments/assets/41a15d56-f4ed-4633-8569-ce84b0aa22bd)

AWS Services Used<br>
AWS IoT Core: Receives MQTT messages from ESP32 over TLS<br>
IoT Rule: Routes incoming messages to Lambda<br>
Lambda: (Python) Processes data, writes to DynamoDB, triggers alerts<br>
DynamoDB: Stores all sensor readings with device + timestamp keys<br>
SNS: Sends email alerts when thresholds are exceeded<br>
API Gateway: REST API for dashboard data retrieval

What I Learned:<br>
Hardware debugging — systematic wire-by-wire verification, I2C address scanning, reading pin labels on microcontrollers<br>
MQTT over TLS — certificate generation, device authentication, IoT Core policies<br>
Serverless architecture — event-driven Lambda triggered by IoT rules, no always-on server required<br>
NoSQL data modeling — DynamoDB partition + sort key design for time-series IoT data<br>
Library compatibility — debugging TLS handshake failures (-5 error) across different MQTT client libraries<br>
AWS region awareness — resources must exist in the same region to communicate<br>

About<br>
Built by Jessica Paradise as part of a hands-on cloud architecture portfolio while pursuing a BS in Computer Science at Western Governors University and studying for the AWS Solutions Architect Associate certification.<br>
Earl is doing great. 🐱
