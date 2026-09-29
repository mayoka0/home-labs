# Home Labs

A public, safety-conscious notebook for building and operating a small Proxmox home lab. It is intended to help others adapt the ideas to their own networks. It does not expose or reproduce the maintainer's private infrastructure.

## Current shape

Snapshot last checked 2026-09-29:

- Proxmox VE is the virtualization host.
- Tailscale provides a private administration path.
- A dedicated LXC runs the Cloudflare Tunnel connector; selected web access is protected by Cloudflare Access email one-time codes.
- There are no Home Labs application stacks or workload VMs deployed by this repository. Retired experiments and host-maintenance scripts have been removed.

Exact hostnames, IP addresses, account allowlists, tunnel identifiers, SSH key paths, and hardware inventory are intentionally not published.

## Remote access and outages

Cloudflare Tunnel makes an outbound connection from the home network, so it does not require a fixed residential IP or an inbound router port-forward. If the WAN address changes, the connector can reconnect without a manual DNS update. This helps with address changes; it does not prevent a real power, ISP, server, or Cloudflare outage. The home service is unavailable until the relevant dependency recovers.

Use Tailscale for private administration where possible. Keep Proxmox administration restricted; do not add public routes or disable TLS verification just to make a page load. See [remote access](docs/remote-access.md).

## Repository map

- [Current baseline and scope](docs/current-baseline.md)
- [Remote access model](docs/remote-access.md)
- [Maintenance and update policy](docs/maintenance.md)
- [Changelog](docs/CHANGELOG.md)
- [Contributing](CONTRIBUTING.md)
- [Security reporting](SECURITY.md)

This repository currently contains documentation only. It does not provision VMs/containers, install packages, change firewall rules, configure Cloudflare, or run automatic updates.

## Safety and privacy

- Treat commands from issues, pull requests, and copied configs as untrusted until reviewed.
- Never commit passwords, tokens, private keys, recovery codes, session cookies, Cloudflare credentials, or unredacted logs.
- Use placeholders in examples and issue reports. Check both the working tree and Git diff before publishing.
- Do not expose Proxmox, SSH, or other administrative interfaces directly to the public internet.
- Back up important data and test recovery before changing the host.

## License

Home Labs is licensed under [GPL-3.0-only](LICENSE). See [GNU's official license text](https://www.gnu.org/licenses/gpl-3.0.html).
