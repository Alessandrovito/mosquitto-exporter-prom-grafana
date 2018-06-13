Prometheus Grafana , Mosquitto Broker and Mosquitto Exporter
========

A monitoring solution for [mosquitto-exporter](https://github.com/Alessandrovito/mosquitto-exporter) with [Prometheus](https://prometheus.io/), [Grafana](http://grafana.org/), 
[Mosquitto Broker](https://github.com/Alessandrovito/docker/tree/master/mosquitto-auth-plugin/1.4.14)

## Install

Clone this repository on your Docker host, cd into mosquitto-exporter-prom-grafana directory and run compose up:

```bash
git clone https://github.com/Alessandrovito/mosquitto-exporter-prom-grafana.git
cd mosquitto-exporter-prom-grafana

docker-compose up -d

or

MOSQUITTO_USER=mosquitto MOSQUITTO_PASSWORD=password docker-compose up -d
```

Containers:

* Prometheus (metrics database) `http://<host-ip>:9090`
* Grafana (visualize metrics) `http://<host-ip>:3000`
* Mosquitto Broker
* Mosquitto-exporter

## Setup Mosquitto-exporter



You can change the credentials in the compose file or by supplying the MOSQUITTO_USER and MOSQUITTO_PASSWORD environment variables on compose up.
Otherwise you can edit docker-compose.yml the environment variable JAVA_OPTS.

`environment:
      - "JAVA_OPTS=-Dlogging.level.com.vitale.exporter.mosquitto=DEBUG -Dmosquitto.exporter.account.username=namemosquitto -Dmosquitto.exporter.account.password=pwmosquitto -Dmosquitto.exporter.broker.name=mosquitto"
`

You can set more variable:
* logging.level.com.vitale.exporter.mosquitto: Logging level for mosquitto-exporter
* mosquitto.exporter.account.username: Account username dedicated to Mosquitto Exporter user
* mosquitto.exporter.account.password: Account password dedicated to Mosquitto Exporter user
* mosquitto.exporter.broker.name: hostname to reach URL Mqtt Broker

## Setup Grafana

Navigate to `http://<host-ip>:3000` and login with user ***admin*** password ***admin***.
Grafana is preconfigured with dashboards ***Mosquitto Broker*** and Prometheus as the default data source:

* Name: Prometheus
* Type: Prometheus
* Url: http://prometheus:9090
* Access: proxy

***Mosquitto Exporter***

![Host](http://www.alessandrovitale.it/images/Screenshot_grafana_mosquitto_exporter.png)

The Mosquitto Broker Dashboard shows key metrics for monitoring the resource usage of your server:

* The number of currently connected, disconnected clients
* The moving average of the number of CONNECT packets received by the broker 
* The total number of messages of any type received,sent and dropped since the broker started.
* The Rate of messages sent and received by Broker
* Publish messages sent, received and dropped by Broker
