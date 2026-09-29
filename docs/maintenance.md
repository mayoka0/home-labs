# Maintenance and updates

## Current state

This repository does not install or enable an automatic update service. The retired Home Labs maintenance scripts and timers were removed; no repo command should be run against the Proxmox host.

## Safe operating policy

- Review the current Proxmox and Debian update guidance before applying host updates.
- Keep backups of important VM/container data and host configuration, and periodically test restoration.
- Apply security updates deliberately. Review Proxmox-related package changes and schedule host restarts manually during a maintenance window.
- Update application containers only after workloads, image versions, backup coverage, and rollback steps have been selected.
- Do not run unreviewed shell scripts, floating-tag bulk upgrades, or unattended hypervisor upgrades on the production host.
- Record what changed and verify Tailscale, the tunnel connector, and intended services afterward.

## Before automating

For each future automation, define its exact target, privileges, schedule and timezone, logs, failure notification, backup/restore plan, and rollback. Test it on a disposable guest before considering the Proxmox host. Never put secrets in this repository or in command-line history.
