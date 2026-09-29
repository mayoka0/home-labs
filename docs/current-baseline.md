# Current baseline

This is a high-level snapshot, not a deployment manifest. It intentionally excludes private identifiers and values.

## Snapshot — 2026-09-29

- The host runs Proxmox VE 9.2.2.
- Tailscale is used as the private administration network.
- A dedicated Linux container runs the Cloudflare Tunnel connector. Selected web access uses Cloudflare Access email one-time codes.
- No Home Labs application stacks or workload VMs are currently managed by this repository.
- This repository contains documentation; it has no scripts or Compose files that install or update software on the host.

The exact domain names, IP addresses, Tailscale identity, Access allowlist, tunnel ID, host hardware, and account details are deliberately omitted. Keep equivalent values in a private inventory or password manager.

## Scope and assumptions

The tunnel connector establishes an outbound connection. A changing residential WAN address does not require a static IP or a manual DNS update for this design. A genuine outage—loss of power, ISP service, the Proxmox host, the connector, or Cloudflare—still makes the home service unavailable until recovery. This is not a high-availability design.

Tailscale is the preferred path for private host administration. Cloudflare Access is an additional identity gate for intentionally published web routes, not a substitute for host security or a reason to expose administrative services broadly.

Before adding a workload, document its purpose, owner, resource limits, backup and restore plan, update policy, and access boundary. Keep machine-specific implementation values out of this public repository.
