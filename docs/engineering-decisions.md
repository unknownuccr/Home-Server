# Key Engineering Decisions

 Several were driven by hardware constraints and by deliberately
optimizing for a working, maintainable system over theoretical best practice. That trade-off is the
honest rationale, not a weakness to hide.

## 1. Self-hosting over a managed cloud / subscription service

- **Decision:** Build and run the automation and security stack on my own hardware, on my own network.
- **Alternatives considered:** Commercial smart-home/security subscriptions, or cloud-hosted equivalents.
- **Reasoning:** I wanted ownership and direct control of my home automation and security, with the
  data and control plane inside my own network rather than dependent on a third party. This is the
  founding decision the rest of the architecture serves.

## 2. Ubuntu Server as the operating system

- **Decision:** Run the platform on Ubuntu (Linux).
- **Alternatives considered:** Other Linux distributions and server operating systems.
- **Reasoning:** Given the constraints of the legacy hardware, Ubuntu was the option most
  straightforward to install and get running reliably on this machine. I prioritized a stable,
  well-supported base I could stand up quickly over a more specialized distribution.

## 3. Docker containers as the deployment model

- **Decision:** Deploy every service as a Docker container rather than installing applications directly on the host.
- **Alternatives considered:** Native/host installation of each application; full virtual machines.
- **Reasoning:** Containers were the deployment model I was proficient with, which let me stand the
  platform up dependably and keep each service isolated and individually manageable. On a single,
  resource-limited host, containers also avoid the overhead of full virtual machines.

## 4. Pi-hole for DNS

- **Decision:** Use Pi-hole as the network-wide DNS resolver and filter.
- **Alternatives considered:** Other DNS / ad-filtering resolvers.
- **Reasoning:** Pi-hole was the resolver I knew how to configure correctly, which mattered for a
  service sitting in the path of all household DNS traffic — a misconfiguration here breaks
  connectivity for every device. Choosing the tool I could deploy and troubleshoot confidently
  reduced that risk.

## 5. SSH-only, LAN-scoped administration with no public exposure

- **Decision:** Administer the server exclusively over SSH from within the local network; expose nothing to the public internet.
- **Alternatives considered:** Port-forwarding SSH or services to the internet for remote access; running a VPN for external entry.
- **Reasoning:** Encrypted SSH is the logical and well-understood administration channel from my
  Windows environment. Keeping it — and the whole platform — confined to the LAN removes the entire
  external attack surface, which is the single largest risk reduction available to a home server.
  The trade-off is no remote access, which I accepted deliberately.
