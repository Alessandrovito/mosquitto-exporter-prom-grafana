dockprom
========

A monitoring solution for Mosquitto Broker with [Prometheus](https://prometheus.io/), [Grafana](http://grafana.org/).

## Install

Clone this repository on your Docker host, cd into dockprom directory and run compose up:

```bash
git clone https://github.com/Alessandrovito/mosquitto-exporter-prom-grafana.git
cd mosquitto-exporter-prom-grafana

docker-compose up -d
```

Containers:

* Prometheus (metrics database) `http://<host-ip>:9090`
* Grafana (visualize metrics) `http://<host-ip>:3000`


## Setup Grafana

Navigate to `http://<host-ip>:3000` and login with user ***admin*** password ***admin***. You can change the credentials in the compose file or by supplying the `ADMIN_USER` and `ADMIN_PASSWORD` environment variables on compose up.

Grafana is preconfigured with dashboards and Prometheus as the default data source:

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
