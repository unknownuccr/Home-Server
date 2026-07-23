# Architecture

![Architecture diagram](../diagrams/architecture.png)

## Overview

The system is a **single physical host** running a Linux operating system (**Ubuntu Server**). All
application workloads run as **Docker containers** on that host; there is no separate hypervisor and
no multi-node cluster. Services communicate locally, and the entire platform is scoped to the home
local-area network, it sits behind the home router and is **not published to the internet**.

Administrative access is performed over **SSH, restricted to the local network**. The host holds a
**static internal IP address** so that its services and SSH endpoint are at a predictable location
on the LAN.

## Component overview

| Layer | Implementation |
|---|---|
| Compute host | Single physical server (Dell XPS 410, repurposed legacy desktop) |
| Operating system | Ubuntu Server (Linux) |
| Runtime layer | Docker — all services run as containers on the host |
| Network position | Behind the home router, on the local network; static internal IP; no public internet exposure |
| Administrative access | SSH, restricted to the LAN |
| DNS | Pi-hole provides network-wide DNS resolution and filtering for the household |
| Messaging backbone | Mosquitto MQTT broker carries messages between automation components |

## Services on the host (all in Docker)

- **Pi-hole** — network-wide DNS resolution and DNS-level filtering for every device on the LAN.
- **Home Assistant** — the home automation platform; the core application the server exists to run.
- **Mosquitto (MQTT)** — lightweight message broker connecting automation devices and services.
- **Uptime Kuma** — self-hosted uptime monitor that watches services and detects outages.
- **Custom status dashboard** — self-built dashboard displaying server and system status.

Three controls run at the **host level** rather than in a container:

- **Fail2ban** — monitors SSH authentication and bans hosts after repeated failed attempts.
- **Host firewall** — default-deny on inbound traffic.
- **tshark** - Wireshark for the terminal.
