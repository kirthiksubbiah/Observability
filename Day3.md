# SRE Learning Log - Metrics Data Requirements

## What is Prometheus?

Prometheus is an open-source monitoring and alerting toolkit widely used for cloud-native observability. It:

- Scrapes metrics from applications at regular intervals.
- Stores them in a time-series database.
- Allows you to query this data using PromQL (Prometheus Query Language).
- Is often paired with Grafana for visualization and Alertmanager for alerts.

---

## Prometheus Metric Types

| Metric Type | Description | Example Use Case |
|-------------|-------------|------------------|
| Counter     | A cumulative value that only increases. | Total number of HTTP requests. Use `rate()` to get the rate over time. |
| Gauge       | A metric that can go up and down. | CPU usage, memory consumption, temperature. |
| Summary     | Captures percentiles (e.g., 95th percentile latency) and count of observations. | Track request latency distribution. |
| Histogram   | Groups values into configurable buckets. Also good for percentiles. | Analyze latency or response time distributions. |

---

## SRE Expectations for Application Metrics

To meet SRE instrumentation standards, your application should:

- Emit metrics aligned with Service Level Indicators (SLIs) such as latency, error rate, and availability.
- Include metrics from all critical system components.
- Expose informational metrics, such as build version or deployment environment.
- Avoid high-cardinality labels (e.g., user ID, session ID) to prevent Prometheus performance issues.

---

## Node Exporter

Node Exporter is a Prometheus exporter that collects host-level metrics such as:

- CPU load
- Memory usage
- Disk I/O
- Filesystem statistics

Prometheus scrapes these metrics from the Node Exporter endpoint to gain visibility into infrastructure performance.

---

## Alerting in SRE

A good alert in an SRE environment should be:

- Precise: It should not fire for non-issues.
- Reliable: It should consistently catch real issues.
- Timely: It should fire quickly when a problem occurs.
- Self-resolving: It should clear automatically once the issue is resolved.

---

## Burn Rate-Based Alerting

Burn rate measures how fast your service is consuming its error budget:

- A burn rate of 1 means normal consumption.
- A burn rate of 10 means the error budget will be exhausted 10 times faster than expected.

### Recommended Burn Rate Alerts

| Alert Type   | Burn Rate Threshold | Time Windows            |
|--------------|---------------------|--------------------------|
| Pager Alert  | Greater than 14.4    | 5 minutes and 1 hour     |
| Ticket Alert | Greater than 3       | 2 hours and 24 hours     |

Using both short and long time windows helps detect both sudden spikes and gradual performance degradations.

---

## Alerting Best Practices

- Use multiple time windows for improved accuracy.
- Pre-compute key metrics to simplify alert rules.
- Tune thresholds to reduce alert fatigue.
- Test alerts by simulating real failure scenarios.

---

## Observability and Incident Management Stack

| Tool         | Purpose                                |
|--------------|----------------------------------------|
| Prometheus   | Metrics collection and storage         |
| Grafana      | Visualization and dashboards           |
| Alertmanager | Alert routing and deduplication        |
| PagerDuty / Opsgenie | On-call management and incident automation |

---

This document is part of my daily SRE/Observability learning notes.
