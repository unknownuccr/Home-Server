# Security Implementation

Security on this platform is built on reducing attack surface and hardening the one administrative entry point. Controls are described at the design level. Operational specifics (addresses, ports, rules) are intentionally omitted from this public repo.

## Implemented and live

- **No public exposure.** The server is not reachable from the public internet. All access is from within the home network.
- **Default-deny firewall.** The host firewall denies inbound traffic by default, permitting only what is explicitly allowed.
- **Fail2ban on SSH.** Fail2ban monitors SSH authentication and bans hosts after repeated failed attempts, blunting brute-force attempts against the admin channel.
- **Credentials kept off the server.** Credentials are not stored on the server itself.
- **Security alerting.** Attempted breaches trigger an immediate push notification via Pushover
  (see [monitoring.md](monitoring.md)).

## limitations 

- **Container-level hardening is not yet implemented** — containers are not currently run as non-root or with read-only filesystems. Tracked in the [roadmap](roadmap.md).
- **No backups exist yet**, so there is no recovery path from a compromise or data-loss event today. Establishing backups and testing a restore is a committed roadmap item.