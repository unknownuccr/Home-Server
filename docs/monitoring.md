# Monitoring & Reliability

## Monitoring & alerting

- **Uptime monitoring.** Uptime Kuma continuously watches the running services and detects when one
  goes offline or fails.
- **Status dashboard.** A self-built dashboard displays live server and system status at a glance.
- **Alerting.** Pushover delivers push notifications on two trigger conditions:
  1. a service going down, and
  2. an attempted security breach.

  This means I learn about both availability and security events without manually checking the system.

## Reliability

- **Automatic service recovery.** All services are configured to restart automatically, so transient
  failures recover without manual intervention.
- **Measured availability.** Observed uptime is **approximately 96%**. I attribute the shortfall
  primarily to **network instability on the server**, a consequence of the aging hardware rather than the service configuration.

## Honest limitations

- There is currently **no backup** of configuration or data, and **no restore has been tested**.
  Establishing backups and validating a restore are committed [roadmap](roadmap.md) items.
- Availability is stated as an **observed approximate figure**, not a guaranteed service level. I
  would rather report ~96% accurately than claim a number I cannot substantiate.

## What I would improve next

The ~96% figure is bounded by hardware, not by the monitoring or recovery design. The highest-value
reliability work is (1) backups + a tested restore, so an outage can't become data loss, and
(2) addressing the network instability at its hardware root. Both are in the roadmap.
