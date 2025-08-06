SRE Requirements for Metrics Data
What is Prometheus?
Prometheus is an open-source monitoring and alerting toolkit widely used for cloud-native observability. It works by scraping metrics from applications at regular intervals, storing them in a time-series database, and allowing you to query this data with PromQL (Prometheus Query Language). It's commonly paired with Grafana for visualization and Alertmanager for handling alerts.

Prometheus Metric Types
Prometheus defines several metric types to handle different kinds of data:

Counter: A cumulative value that only ever increases. It's used for things like the total number of requests served. You can use the rate() function to calculate a counter's rate of increase over time.

Gauge: A metric that can go up and down, like the current CPU utilization or temperature.

Summary: Captures percentiles (e.g., 95th percentile latency) and a count of observations. It's useful for measuring performance characteristics.

Histogram: Similar to a Summary, it groups values into configurable buckets. This is ideal for analyzing the distribution of latency or response times.

SRE Expectations for Application Metrics
For an application to be considered well-instrumented by SRE standards, it should:

Emit metrics that are aligned with your Service Level Indicators (SLIs), such as latency, error rates, and availability.

Include metrics from all critical components of the system.

Expose informational metrics like the application's build version and deployment environment.

Avoid high-cardinality labels (e.g., user IDs or session IDs) to prevent performance issues in Prometheus.

Node Exporter
The Node Exporter is a tool that collects host-level metrics from a server, like CPU load, memory usage, disk I/O, and filesystem statistics. Prometheus scrapes this data from the exporter's endpoint to provide insights into the underlying infrastructure.

Alerting in SRE
A good alert in an SRE context should be:

Precise: It should not fire for non-issues.

Reliable: It should catch actual problems consistently.

Timely: It should fire quickly when an issue arises.

Self-resolving: It should automatically resolve once the issue is fixed.

Burn Rate-Based Alerting
Burn rate is a key concept in SRE alerting. It measures how fast you're consuming your error budget.

A burn rate of 1 means you're consuming your error budget at the normal rate.

A burn rate of 10 means you're consuming your budget 10 times faster than normal, suggesting you'll run out of budget in about 3 days.

Recommended burn rate alerts include:

Pager Alerts: For critical issues, fire an alert when the burn rate is greater than 14.4 over short (e.g., 5-minute) and long (e.g., 1-hour) time windows.

Ticket Alerts: For less urgent issues, create a ticket when the burn rate is greater than 3 over 2-hour and 24-hour windows.

Using both short and long time windows helps detect sudden spikes in errors as well as slow, gradual degradations.

Alerting Best Practices
Use multiple time windows for more accurate alerting.

Pre-compute key metrics to simplify your alerting rules.

Tune your alert thresholds carefully to avoid alert fatigue.

Test your alerts by simulating failures.

Observability and Incident Management
An effective observability stack is built on several key tools:

Prometheus for metric scraping and storage.

Grafana for dashboarding and data visualization.

Alertmanager for routing alerts and notifications.

For incident management, tools like Opsgenie and PagerDuty are used for on-call scheduling, automated workflows, and escalating alerts.
