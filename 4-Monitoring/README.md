# 4. Monitoring

## Goal

In this exercise, you will set up a monitoring stack for the application.

By the end of the exercise, you will have learned how to use Prometheus and Grafana to monitor a containerized application.

## Task Overview

You will configure and set up:

- cAdvisor as the data collector
- Prometheus as the time-series database
- Grafana as the data visualization tool

## 1. Write the Prometheus configuration file

Create a new directory at the root of the repository to manage the monitoring stack and create a Prometheus configuration file inside.

```bash
mkdir monitoring
cd monitoring
touch prometheus.yml
```

Here are the steps you'll have to complete. For each one, try to find and use the correct keywords by referring to the official Prometheus starting guide:
<https://prometheus.io/docs/prometheus/latest/getting_started/#configuring-prometheus-to-monitor-itself> and configuration documentation <https://prometheus.io/docs/prometheus/latest/configuration/configuration/>.

- Global configuration
  - Set a global scrape_interval, for example every 60 seconds.
- Scraping jobs
  - Configure Prometheus to scrape its own metrics.
    Target: `localhost:9090`
  - cAdvisor: configure Prometheus to scrape container metrics via cAdvisor.
    Target: `cadvisor:8080`

**Solution**: Will be provided

## 2. Start the monitoring stack

First, create a Docker network for the monitoring stack

```bash
docker network create monitoring
```

Start cAdvisor.

```bash
sudo docker run \
  --volume=/:/rootfs:ro \
  --volume=/var/run:/var/run:rw \
  --volume=/sys:/sys:ro \
  --volume=/var/lib/docker/:/var/lib/docker:ro \
  --publish=8080:8080 \
  --detach=true \
  --name=cadvisor \
  --network=monitoring \
  gcr.io/cadvisor/cadvisor:v0.52.0 
```

Start Prometheus.

```bash
docker run \
    -d \
    -p 9090:9090 \
    -v ./prometheus.yml:/etc/prometheus/prometheus.yml \
    --name=prometheus \
    --network=monitoring \
    prom/prometheus:v2.53.4
```

Start Grafana.

```bash
docker run -d -p 4000:3000 --name=grafana --network=monitoring grafana/grafana:11.5.4
```

> [!IMPORTANT]
> As no Docker volume has been configured, deleting the Prometheus or Grafana containers will delete any data inside it (metrics, dashboards, ...) !

## Configure Grafana

Connect to Grafana at <http://localhost:4000>.
The default credentials are `admin` / `admin`.

Set Prometheus as a data source, by following this documentation <https://grafana.com/docs/grafana/latest/datasources/prometheus/configure-prometheus-data-source/>.
Prometheus url is `http://prometheus:9090`.

Import the Grafana dashboard with ID `14282` by following this documentation <https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/import-dashboards/>.

Take a look at how queries are made and try to build your own panel !

## 🎉 Congratulations

**You've completed the last exercise !**
