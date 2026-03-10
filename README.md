# IoT Sensor Monitoring System (ESP32 + MQTT + Docker)

## Project Overview

This project demonstrates a complete **IoT data pipeline** for collecting environmental sensor data using an ESP32 microcontroller and visualizing it in a real-time dashboard.

The system reads temperature and humidity data from a DHT sensor connected to an ESP32 and sends the data using the MQTT protocol to a cloud-ready IoT backend running inside Docker containers.

The backend stack includes an MQTT broker, data processing layer, time-series database, and a visualization dashboard.

This project is designed as a **learning and testing platform for building scalable IoT architectures** that can later be deployed to a VPS or cloud server.

---

## System Architecture

ESP32 + DHT Sensor
↓
MQTT Protocol
↓
EMQX MQTT Broker
↓
Node-RED Data Processing
↓
InfluxDB Time-Series Database
↓
Grafana Dashboard

---

## Technologies Used

### Hardware

* ESP32 Microcontroller
* DHT11 / DHT22 Temperature and Humidity Sensor

### Software

* Docker & Docker Compose
* EMQX MQTT Broker
* Node-RED
* InfluxDB
* Grafana
* Arduino IDE

---

## Features

* Real-time sensor data collection
* MQTT-based communication
* Containerized IoT backend using Docker
* Time-series data storage
* Real-time data visualization
* Modular architecture suitable for scaling to cloud deployment

---

## Project Structure

```
iot-server/
│
├── docker-compose.yml
├── README.md
│
├── esp32_code/
│   └── esp32_dht_mqtt.ino
│
└── nodered_flows/
    └── flow.json
```

---

## Hardware Setup

Connect the DHT sensor to the ESP32 as follows:

| Sensor Pin | ESP32 Pin |
| ---------- | --------- |
| VCC        | 3.3V      |
| GND        | GND       |
| DATA       | GPIO4     |

---

## Backend Setup (Docker)

Make sure Docker and Docker Compose are installed.

Run the following command inside the project directory:

```
docker compose up -d
```

This will start the following services:

| Service          | Port  |
| ---------------- | ----- |
| EMQX MQTT Broker | 1883  |
| EMQX Dashboard   | 18083 |
| Node-RED         | 1880  |
| InfluxDB         | 8086  |
| Grafana          | 3000  |

---

## Access the Services

EMQX Dashboard
http://localhost:18083

Node-RED
http://localhost:1880

InfluxDB
http://localhost:8086

Grafana
http://localhost:3000

---

## ESP32 Configuration

Update the WiFi and MQTT broker settings in the ESP32 code:

```
const char* ssid = "YOUR_WIFI_NAME";
const char* password = "YOUR_WIFI_PASSWORD";
const char* mqtt_server = "YOUR_COMPUTER_IP";
```

Sensor data is published to the MQTT topic:

```
sensor/dht11
```

Example payload:

```
{
 "temperature": 29.5,
 "humidity": 70
}
```

---

## Node-RED Flow

The Node-RED flow performs the following actions:

1. Subscribe to MQTT topic `sensor/dht11`
2. Parse the incoming JSON data
3. Store the data in InfluxDB
4. Forward the data for dashboard visualization

---

## Grafana Dashboard

Grafana connects to InfluxDB to visualize the sensor data.

Example panels:

* Temperature Graph
* Humidity Graph
* Real-time sensor monitoring

---

## Future Improvements

* MQTT authentication and TLS security
* Cloud deployment on a VPS
* Mobile application integration
* Multi-device sensor monitoring
* Alert system for abnormal sensor readings

---

## Learning Goals

This project was created to learn and practice:

* IoT system architecture
* MQTT messaging
* Docker containerization
* Time-series data storage
* Real-time monitoring dashboards

---

## License

This project is open-source and intended for educational purposes.
