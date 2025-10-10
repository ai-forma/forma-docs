# Observability and Monitoring

Observability is built into every Forma container image.  
By default, agents ship with [OpenTelemetry](https://opentelemetry.io/) instrumentation, extended with [OpenInference](https://arize-ai.github.io/openinference) standards.  

This means:
- You can send traces, logs, and metrics to **any OTEL-compatible backend** (Grafana, Tempo, Datadog, etc.).
- You can analyze AI-specific traces with [Phoenix Arize](https://phoenix.arize.com).
- You can integrate Forma agents into your existing observability stack with no additional coding.

---

## What We Collect

- **Traces** – Each request and workflow execution is traced, including LLM calls and tool invocations.  
- **Metrics** – Counters and histograms for request counts, latencies, and error rates.  
- **Logs** – Structured logs at configurable levels (`trace`, `debug`, `info`).  

We intentionally **do not log our dependencies** (like LLM provider SDKs). Instead, we propagate their errors and report them in a clean, standardized way. That way, your logs reflect *your agent’s behavior*, not library internals.

---

## Configuration

You can configure observability via environment variables when running your container.

### OTEL Collector

Point your agent to an OpenTelemetry Collector (local or remote):

```sh
# gRPC endpoint (default)
export OTEL_EXPORTER_OTLP_ENDPOINT="http://localhost:4317"

# Optional: separate metrics endpoint
export OTEL_EXPORTER_OTLP_METRICS_ENDPOINT="http://localhost:4317/v1/metrics"
```

## Log Levels

Control the verbosity of Forma logs with AI_LOGS variables:

## Options: trace | debug | info (default)

```sh
export AI_LOGS=debug
```

* trace – Most detailed, includes every span and step.
* debug – Useful for development; shows workflow decisions and tool calls.
* info – Production-friendly; high-level events and errors only.

### Quick Start with Phoenix

If you want to analyze AI-specific traces:
* Run a local Phoenix Arize instance (Dockerized).
* Point OTEL_EXPORTER_OTLP_ENDPOINT to it.
* Interact with your agent and watch traces appear in Phoenix.