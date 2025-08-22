# Docker Host Monitoring with Prometheus, Telegraf, and InfluxDB

This project provides a complete monitoring solution for a Docker host using a stack of popular open-source tools. It collects metrics about all running containers, triggers alerts on specific conditions (like high CPU or container stops), and provides a platform for visualizing the data.

## Features

- **Container Metrics:** Collects detailed metrics from all containers running on the host, including CPU, memory, network, and state.
- **Alerting:** Pre-configured alerts for common issues like high CPU usage and containers going down.
- **Visualization:** Includes Grafana for building dashboards to visualize container performance over time.
- **Long-term Storage:** Uses InfluxDB for storing metrics data.
- **All-in-One:** Packaged as a single `docker-compose` setup for easy deployment.

## Services

The following services are included in this monitoring stack:

| Service      | Port | Description                                      |
|--------------|------|--------------------------------------------------|
| **Prometheus** | 9090 | Scrapes and stores metrics, evaluates alert rules. |
| **Alertmanager**| 9093 | Handles alerts sent by Prometheus.               |
| **Telegraf**   | -    | Collects container metrics from the Docker daemon. |
| **InfluxDB**   | 8086 | Long-term storage for metrics data.              |
| **Grafana**    | 3000 | For visualizing metrics in dashboards.           |


## How to Run

### Prerequisites

- Docker
- Docker Compose

### 1. Start the Monitoring Stack

Navigate to the project's root directory and run the following command to start all services in the background:

```bash
docker-compose up -d
```

### 2. Access the Services

Once the containers are running, you can access the different services via your web browser:

- **Prometheus:** [http://localhost:9090](http://localhost:9090)
  - Check the **Targets** page to ensure Telegraf is being scraped successfully.
  - Check the **Alerts** page to see the status of configured alerts.

- **Alertmanager:** [http://localhost:9093](http://localhost:9093)
  - View and manage active alerts.

- **Grafana:** [http://localhost:3000](http://localhost:3000)
  - Default login: `admin` / `admin` (you will be prompted to change the password on first login).
  - From here, you can add Prometheus as a data source and build dashboards to visualize the container metrics.

- **InfluxDB:** [http://localhost:8086](http://localhost:8086)
  - You can interact with the raw time-series data using the credentials from the `docker-compose.yaml` file.

### 3. Stop the Stack

To stop all the services, run:

```bash
docker-compose down
```

To clean all data:

```bash
docker volume rm prometheus-monitor_alertmanager_data prometheus-monitor_grafana-data prometheus-monitor_grafana_data prometheus-monitor_influxdb_data prometheus-monitor_prometheus_data
```
