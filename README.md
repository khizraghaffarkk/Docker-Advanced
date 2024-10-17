# Toyota Data Feeder with Mosquitto MQTT

This project is a simple Dockerized data feeder application that sends data to an MQTT broker (Mosquitto) over secured TLS/SSL communication. The setup includes two main services:
- **Toyota Data Feeder**: A Python application that feeds data to the MQTT broker.
- **Mosquitto MQTT Broker**: A popular open-source MQTT broker with TLS/SSL support for secure communication.

## Table of Contents
- [Project Overview](#project-overview)
- [Prerequisites](#prerequisites)
- [Setup](#setup)
  - [Docker Compose](#docker-compose)
  - [Mosquitto Configuration](#mosquitto-configuration)
- [Project Files](#project-files)
- [How to Run](#how-to-run)
- [License](#license)

## Project Overview

The purpose of this project is to securely send vehicle data from a Python script to a Mosquitto MQTT broker using Docker containers. It uses TLS/SSL for secure communication between the data feeder and the broker.

## Prerequisites

To run this project, you need to have the following installed on your system:

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)

## Setup

### Docker Compose

The `docker-compose.yml` file defines two services:
1. **toyota-data-feeder**: Sends vehicle data to the MQTT broker using a Python script (`feeder.py`).
2. **mosquitto**: The MQTT broker that listens on two ports, 1883 (non-secure) and 8883 (TLS/SSL-secured).

The `compose` file also sets up a custom network named `khghaffa23-net` for communication between the services.

### Mosquitto Configuration

The `mosquitto.conf` file is mounted into the Mosquitto container, defining the following configurations:
- Listeners on ports 1883 (plain MQTT) and 8883 (TLS/SSL MQTT).
- Certificates for SSL encryption, mounted as volumes in the container:
  - `server.crt`: Server certificate.
  - `server.key`: Server private key.
  - `ca.crt`: Certificate authority.

## Project Files

- `.gitignore`: Defines files that are ignored by Git.
- `Dockerfile`: Builds the `toyota-data-feeder` image.
- `ca.crt`, `server.crt`, `server.key`: Certificates for securing the Mosquitto broker.
- `feeder.py`: Python script that feeds data to the MQTT broker.
- `requirements.txt`: Python dependencies for the `feeder.py` script.
- `toyota_data.csv`: Sample vehicle data that the script reads and sends to the broker.
- `mosquitto.conf`: Configuration file for the Mosquitto broker.

## How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/khizraghaffarkk/toyota-data-feeder.git
   cd toyota-data-feeder
2. Build and start the services using Docker Compose:
   docker-compose up --build

3. The Mosquitto broker will be available on the following ports:

- `Port 1883: Plain MQTT
- `Port 8883: Secure MQTT with TLS/SSL
4. The feeder.py script will start sending vehicle data to the Mosquitto broker over the secure MQTT connection.
