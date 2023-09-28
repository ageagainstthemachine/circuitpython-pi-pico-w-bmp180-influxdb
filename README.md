# A CircuitPython Pi Pico W BMP180 InfluxDB Example
A CircuitPython example using asyncio cooperative multitasking for the Raspberry Pi Pico W which sends data from a BMP180 sensor to an InfluxDB v2 server.

## Requirements
- Raspberry Pi Pico W running CircuitPython 8.2.x (tested on 8.2.6)
- BMP180 sensor
- InfluxDB v2 server with configured bucket and API key
- The following CircuitPython libraries are used:
    - board
    - digitalio
    - wifi
    - socketpool
    - bmp180
    - adafruit_ntp
    - time
    - asyncio
    - supervisor
    - os
    - busio
    - adafruit_requests
    - ssl
    - usyslog

## Notes
This example was developed using the asyncio cooperative multitasking method in order to allow several tasks to function independently and at different loop intervals. Basic UDP syslog functionality is incorporated as well for the purposes of being able to allow troubleshooting without having the serial cable connected. The syslog functionality can be enabled or disabled.

These tasks are:
- Reading the BMP180 sensor
- Connect to the WiFi
- NTP time sync
- Send data to InfluxDB

Loading the various settings at runtime is achieved by the settings.toml file method. The following are the settings:

    ssid = "SSID_HERE"
    psk = "PSK_HERE"
    INFLUXDB_URL = "https://example.fqdn.com/api/v2/write"
    INFLUXDB_ORG = "ORG"
    INFLUXDB_BUCKET = "CircuitPythonTest"
    INFLUXDB_TOKEN = "INFLUX_TOKEN_HERE"
    SYSLOG_SERVER = "10.0.0.10"
    SYSLOG_SERVER_ENABLED = "FALSE"
    SYSLOG_PORT = 514

WiFi reconnection is also incorporated and the WiFi task automatically checks to determine if it the device is still connected and if not, attempts to reconnect to the specified network.

HTTP POST is used for getting the metrics to the InfluxDB v2 server.

## Disclaimer
This example is probably unstable and full of bugs. Like everything else on the internet, run/use at your own risk.