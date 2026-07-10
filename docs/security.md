# Security Implementation

Security on this platform is built on **reducing attack surface** and **hardening the one
administrative entry point**, rather than on bolt-on tooling. Controls are described at the design
level; operational specifics (addresses, ports, rules) are intentionally omitted from this public repo.

## Implemented and live

- **No public exposure.** The server is not reachable from the public internet. All access is from
  within the home network, which eliminates remote attack surface by design. This is the platform's
  single strongest security property.
- **Two-factor SSH login.** SSH access requires **both** a valid SSH key **and** a password — two
  independent factors must be satisfied to authenticate.
- **Default-deny firewall.** The host firewall denies inbound traffic by default, permitting only
  what is explicitly allowed.
- **Fail2ban on SSH.** Fail2ban monitors SSH authentication and bans hosts after repeated failed
  attempts, blunting brute-force attempts against the admin channel.
- **Credentials kept off the server.** Credentials are not stored on the server itself.
- **Security alerting.** Attempted breaches trigger an immediate push notification via Pushover
  (see [monitoring.md](monitoring.md)).

## Honest limitations

These are real and disclosed rather than papered over:

- **Container-level hardening is not yet implemented** — containers are not currently run as
  non-root or with read-only filesystems. Tracked in the [roadmap](roadmap.md).
- **No backups exist yet**, so there is no recovery path from a compromise or data-loss event today.
  Establishing backups and testing a restore is a committed roadmap item.

I do not claim a control I have not configured.

## Why this posture is defensible

For a single-host home server, the highest-leverage security move is **not exposing it to the
internet at all** — which removes the entire class of remote attacks before any other control
matters. The remaining hardening (two-factor SSH, default-deny firewall, Fail2ban) protects the
one entry point that does exist: LAN-based SSH administration. The posture is matched to the real
threat model rather than padded with controls that wouldn't change the outcome.
