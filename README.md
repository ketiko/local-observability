# opentelemetry-docker-compose

Docker setup for running OpenTelemetry observability tooling locally

## What this does

This provides a docker compose configuration for running OpenTelemetry tools locally. This includes:

1. An OpenTelemetry Collector
2. Prometheus for storing metrics
3. Tempo for storing traces
4. Loki for storing logs
5. Grafana for visualizing everything

## Getting Started

### Start the stack

```bash
docker compose up
```

### Point your OpenTelemetry instrumented application to the collector

The OpenTemetry Collector is running on the default urls of http://localhost:4317 and http://localhost:4318.

If your SDK supports sending OTLP logs, they will also show up in Grafana.

### Run your application and collect data

Optionally, you can generate fake traces to see how it works before wiring up your application.

```bash
docker compose -f compose.generate-traces.yml up
```

### Open Grafana and view your traces, metrics, and logs

Visit http://localhost:3000/explore to explore the data in Grafana.

Some sample dashboards are included.

Optionally, if the default Grafana port of `3000` conflicts with your application you can set the `GRAFANA_PORT` environment variable.

```bash
# Add .env file
GRAFNANA_PORT=[new port]
```
