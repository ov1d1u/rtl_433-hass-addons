# rtl_433 Home Assistant Add-on

## About

This add-on is a simple wrapper around the [modded rtl_433](https://github.com/halfbakery/rtl_433/tree/mqtt_rfraw_support) project that receives wireless sensor data via Sonoff RF Bridge, flashed with Tasmota and [additional EFM8BB1 firmware](https://github.com/halfbakery/RF-Bridge-EFM8BB1/tree/rebaked_sniffer), decodes and outputs it to MQTT.

[View the rtl_433 documentation](https://triq.org/rtl_433)

## How it works

The only thing this add-on does is run rtl_433 under the Home Assistant OS supervisor.

By default, modded rtl_433 prints the data it receives to the terminal and publishes the data back to MQTT so that Home Assistant can access it.

Once you get the rtl_433 sensor data into MQTT, you'll need to help Home Assistant discover and make sense of it. You can do that in a number of ways:

  * manually configure `sensors` and `binary_sensors` in HA and [link them to the appropriate MQTT topics](https://www.home-assistant.io/integrations/sensor.mqtt/) coming out of rtl_433,
  * run the [rtl_433_mqtt_hass.py](https://github.com/merbanan/rtl_433/tree/master/examples/rtl_433_mqtt_hass.py) script manually or on a schedule to do most of the configuration automatically, or
  * install the [rtl_433 MQTT Auto Discovery Home Assistant Add-on](https://github.com/pbkhrv/rtl_433-hass-addons/tree/main/rtl_433_mqtt_autodiscovery), which runs rtl_433_mqtt_hass.py for you.

## Prerequisites

 To use this add-on, you need the following:

 1. Sonoff RF Bridge with Tasmota and [halfbakery's firmware](https://github.com/halfbakery/RF-Bridge-EFM8BB1/tree/rebaked_sniffer) for EFM8BB1.
    In order to start sniffing automatically you have to create a rule in Tasmota's console and enable it via commands:
    ```
    Rule1 on system#boot do RfRaw 177 endon
    Rule1 1
    ```
    First command creates rule to start RfRaw 177 and second command enables that rule.

 2. Home Assistant OS running on a machine with.

 3. Some wireless sensors supported by rtl_433. The full list of supported protocols and devices can be found under "Supported device protocols" section of the [rtl_433's README](https://github.com/merbanan/rtl_433/blob/master/README.md).

## Installation

 0. Flash and configure your Sonoff RF Bridge

 1. Install the add-on.

 2. Configure the add-on

 3. Start the add-on and check the logs.

## Configuration

  * `mqtt_host`
  * `mqtt_port`
  * `mqtt_user`
  * `mqtt_password`
  * `tasmota_topic`: MQTT topic where Sonoff RF Bridge is publishing its output. Default is "tele/tasmota_XXXXXX/RESULT".

## Credit

This add-on is based on James Fry's [rtl4332mqtt Hass.IO Add-on](https://github.com/james-fry/hassio-addons/tree/master/rtl4332mqtt), which is in turn based on Chris Kacerguis' project here: [https://github.com/chriskacerguis/honeywell2mqtt](https://github.com/chriskacerguis/honeywell2mqtt), which is in turn based on Marco Verleun's rtl2mqtt image here: [https://github.com/roflmao/rtl2mqtt](https://github.com/roflmao/rtl2mqtt).
