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
./start-observability.sh
```

### Point your OpenTelemetry instrumented application to the collector

The OpenTemetry Collector is running on the default urls of http://localhost:4317 and http://localhost:4318.

If your SDK supports sending OTLP logs, they will also show up in Grafana.

###  Instrument your application and collect data
#### Java

To instrument your Java application, set the following environment variables and launch your application.

The opentelemetry-javaagent.jar is included in this repository.

```bash
EXPORT JAVA_OPTS="-javaagent:./path/to/this/repository/opentelemetry-javaagent.jar"
EXPORT OTEL_EXPORTER_OTLP_ENDPOINT="http://localhost:4317"
EXPORT OTEL_SERVICE_NAME="my-app-name"
```

#### Node.js

To instrument your Node.js application, install the following npm packages and the environment variable. Then launch your application.

```bash
npm install @opentelemetry/sdk-node \
  @opentelemetry/api \
  @opentelemetry/auto-instrumentations-node \
  @opentelemetry/sdk-metrics \
  @opentelemetry/sdk-trace-node

EXPORT NODE_OPTIONS="--require '@opentelemetry/auto-instrumentations-node/register'"
EXPORT OTEL_EXPORTER_OTLP_ENDPOINT="http://localhost:4317"
EXPORT OTEL_SERVICE_NAME="my-app-name"
```

Random traces are generated automatically to show sample data in addition to your own application.

### Open Grafana and view your traces, metrics, and logs

Visit http://localhost:3050/d/opentelemetry-apm/opentelemetry-apm to explore the data in Grafana.

Optionally, if the default Grafana port of `3050` conflicts with your application you can set the `GRAFANA_PORT` environment variable.

```bash
# Add .env file
GRAFNANA_PORT=[new port]
```
