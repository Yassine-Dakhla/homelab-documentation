# Networking

## Network Overview

The homelab uses a private LAN behind the home router.

Proxmox provides a virtual bridge for networking between the host and its guests.

## Main Network

| Component | Configuration |
|---|---|
| Proxmox bridge | vmbr0 |
| LAN network | 192.168.11.0/24 |
| Proxmox host | 192.168.11.140 |
| Gateway | 192.168.11.1 |

Services running in containers use their own LAN addresses.

## Virtual Networking

The Proxmox host uses **vmbr0** as the main virtual network bridge. This allows LXC containers and VMs to communicate with the physical LAN through the host's network interface.

## Remote Access

Tailscale is used for remote access instead of exposing homelab services directly to the public Internet.

This keeps the lab accessible remotely without relying on direct port forwarding for internal services.

## Networking Skills Practiced

- IPv4 addressing
- Subnetting
- Static IP configuration
- Linux networking
- Proxmox bridges
- LXC networking
- Remote access with Tailscale
- Basic network troubleshooting
