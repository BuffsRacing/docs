# Visualisation

## Logging

During the race, the Pi-4 has a web-server that can be used to read logs from the telemetry and streaming software. An alternative for viewing logs from the mobile app might be implemented in the future.

## Streaming

With both the app and the Pi, we have configured it to stream to twitch. 
We are in the process of setting up an official Twitch channel, 
but in the meanwhile during races the stream can be accessed at [https://twitch.tv/prudentwish](https://twitch.tv/prudentwish)

## Telemetry

We use the free hosted instance of Grafana for our dashboard. The data is sent to the Graphite server and then visualised using our template. The dashboard has an option to choose which car the data needs to be shown for.

The dashboard currently shows the following data:

* GPS

* Race Stats

* Twitch Stream

* OBD-II Data