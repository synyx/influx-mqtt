# Influx-mqtt #

This application is an MQTT client which can subscribe to multiple topics, writing each message's payload into an InfluxDB instance using its HTTP-based line-protocol.

## Features ##

- Subscribes to all topics specified in the configuration file.
- Supports HTTP and HTTPS.
- Uses last part of topic name for Influx series name.
- Based on libmosquitto (MQTT) and POCO (HTTP(S)).
- Written in C++.
- Simple Make-based project.

## Payload format ##

The payload format format for an MQTT message is expected to have this format:

*[location];[value]*

## InfluxDB line protocol format ##

These MQTT payload values are then parsed and written to the InfluxDB in this format:

URL: *[InfluxDB URL]/write?db=[DB name]*

POST data:

*[series],location=[location] value=[value]*



> Please note that the Influx Line Protocol does not support spaces and similar. As this service currently does not escape these characters, adding spaces to a location or value will result in the InfluxDB write failing.

## Building the application ##

In order to build the Influx-mqtt service, one needs to have these dependencies installed:

- g++ (C++ compiler)
- libmosquittopp (C++ wrapper for libmosquitto)
- libmosquitto (C MQTT library)
- POCO libraries (HTTP and text parsing)
- OpenSSL (for HTTPS)

Simply execute the following command in the folder with the Makefile:

    make

This should build and link the project, creating a single 'influx_mqtt' library.

Building the code has been tested on OS X and Linux (Ubuntu 14.04LTS, 16.04LTS, Debian (stable).
