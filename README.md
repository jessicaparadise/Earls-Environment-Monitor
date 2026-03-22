Earl's Environment Monitor
A real-time IoT environmental monitoring system built with an ESP32 microcontroller and AWS cloud infrastructure. Tracks temperature and humidity conditions in my cat Earl's room, with live OLED display, cloud data storage, and automated email alerts.

 Phase 1 — Hardware + OLED display
 Phase 2 — AWS IoT Core MQTT connection
 Phase 3 — DynamoDB storage
 Phase 4 — SNS email alerts
 Phase 5 — REST API + web dashboard

 Architecture
 DHT11 Sensor → ESP32 → WiFi → AWS IoT Core
                  ↓                  ↓
             OLED Display        IoT Rule
                                     ↓
                                  Lambda
                                 ↓       ↓
                             DynamoDB   SNS
                                         ↓
                                   Email Alert
Hardware
ELEGOO ESP32
DHT11
SSD1306 OLED
Breadboard

Wiring:
DHT11 S → ESP32 GPIO4
DHT11 + → 3.3V rail
DHT11 − → GND rail
OLED SDA → ESP32 GPIO21
OLED SCL → ESP32 GPIO22
OLED VCC → 3.3V rail
OLED GND → GND rail
![Untitled](https://github.com/user-attachments/assets/41a15d56-f4ed-4633-8569-ce84b0aa22bd)

AWS Services Used
AWS IoT Core: Receives MQTT messages from ESP32 over TLS
IoT Rule: Routes incoming messages to Lambda
Lambda: (Python) Processes data, writes to DynamoDB, triggers alerts
DynamoDB: Stores all sensor readings with device + timestamp keys
SNS: Sends email alerts when thresholds are exceeded
API Gateway: REST API for dashboard data retrieval

What I Learned:
Hardware debugging — systematic wire-by-wire verification, I2C address scanning, reading pin labels on microcontrollers
MQTT over TLS — certificate generation, device authentication, IoT Core policies
Serverless architecture — event-driven Lambda triggered by IoT rules, no always-on server required
NoSQL data modeling — DynamoDB partition + sort key design for time-series IoT data
Library compatibility — debugging TLS handshake failures (-5 error) across different MQTT client libraries
AWS region awareness — resources must exist in the same region to communicate

About
Built by Jessica Paradise as part of a hands-on cloud architecture portfolio while pursuing a BS in Computer Science at Western Governors University and studying for the AWS Solutions Architect Associate certification.
Earl is doing great. 🐱
