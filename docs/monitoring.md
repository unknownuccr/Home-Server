# Monitoring & Reliability

## Monitoring & alerting

- **Uptime monitoring.** Uptime Kuma continuously watches the running services and detects when one goes offline or fails.
- **Status dashboard.** A dashboard displays live server and system status at a glance.
- **Alerting.** Pushover delivers push notifications on two trigger conditions:
  1. a service going down.
  2. an attempted security breach.


## Reliability

- **Automatic service recovery.** All services are configured to restart automatically, so transient failures recover without manual intervention.
- **Measured availability.** Observed uptime is **approximately 96%**. I have observed this number to be primarily because of **network instability on the server**, a consequence of the aging hardware.