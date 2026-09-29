# Remote access

This document describes the access pattern without publishing the maintainer's hostnames, addresses, identity allowlist, or credentials.

## Private administration

Use Tailscale to reach the Proxmox host privately, then SSH with a key. A local shortcut can be defined in the operator's own SSH config:

```sshconfig
Host lab
    HostName <your-proxmox-tailnet-name>
    User <your-admin-user>
    IdentityFile ~/.ssh/<your-private-key>
    IdentitiesOnly yes
    ServerAliveInterval 30
    ServerAliveCountMax 3
```

Replace every placeholder locally. Do not commit your SSH config or private key. Prefer a dedicated administrative identity with only the privileges it needs; keep SSH reachable only over the LAN or private tailnet. Keep host-key checking enabled.

## Web access through Cloudflare

The current design uses a Cloudflare Tunnel connector in a dedicated Linux container and Cloudflare Access as an identity gate for selected web routes. The connector makes an outbound connection, so this pattern does not need an inbound router port-forward or a fixed residential IPv4 address. After a WAN address change, the connector should reconnect; no hand-maintained A record for the home address is part of this design.

The actual public hostnames, Access email allowlist, tunnel ID, connector token, and origin addresses are private configuration and must not be added here. Store tunnel credentials outside Git with restrictive file permissions. Require an explicit Access policy; never create a bypass policy for convenience.

Use Tailscale for Proxmox administration whenever practical. If a web route to an administrative interface is intentionally retained, restrict it to known identities, use strong account authentication and MFA where supported, keep the host patched, and test that unauthenticated requests are denied. A Cloudflare Access login page is an extra control, not a replacement for those safeguards.

## Availability limits

A tunnel helps absorb a changing home IP because the connector calls out to Cloudflare. It cannot keep a service online through loss of power, home internet, the Proxmox host, the connector container, or a Cloudflare incident. Monitoring and recovery procedures can shorten detection and recovery time, but do not turn a single-server home lab into a highly available service.
