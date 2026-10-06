# LXC Containers

The homelab uses three Ubuntu LXC containers on the Proxmox host. Each container has a specific role, keeping services separated while sharing the host's storage and network.

## Container Overview

| ID | Hostname | CPU | RAM | Root Disk | Role |
|---|---|---:|---:|---:|---|
| 100 | media | 2 cores | 2 GB | 40 GB | Jellyfin media server |
| 101 | File-Server | 1 core | 512 MB | 8 GB | Samba file server |
| 102 | Docker-arr-stack | 2 cores | 2 GB | 20 GB | Docker media automation stack |

All three containers use:

- Ubuntu 24.04 LTS
- Unprivileged LXC
- `vmbr0` networking
- Static LAN addressing
- 512 MB swap
- Proxmox firewall enabled on the network interface

## LXC 100 — media

**Purpose:** Media streaming with Jellyfin.

| Resource | Configuration |
|---|---|
| CPU | 2 cores |
| RAM | 2 GB |
| Root disk | 40 GB |
| LAN IP | 192.168.11.141/24 |
| Storage mount | `/mnt/hdd/media → /media/storage` |

The container has Intel integrated graphics passed through from the Proxmox host for Jellyfin hardware-accelerated media processing.

It also has access to the Linux TUN device for networking requirements.

### Main Service

- Jellyfin — port 8096

## LXC 101 — File-Server

**Purpose:** Network file sharing.

| Resource | Configuration |
|---|---|
| CPU | 1 core |
| RAM | 512 MB |
| Root disk | 8 GB |
| LAN IP | 192.168.11.142/24 |
| Storage mount | `/mnt/hdd/media → /media` |

The container runs Samba and provides access to the shared media storage over the local network.

### Main Service

- Samba — ports 139 and 445

## LXC 102 — Docker-arr-stack

**Purpose:** Run the media automation and library management stack using Docker.

| Resource | Configuration |
|---|---|
| CPU | 2 cores |
| RAM | 2 GB |
| Root disk | 20 GB |
| LAN IP | 192.168.11.143/24 |
| Storage mount | `/mnt/hdd/media → /media/storage` |

Docker is installed inside this unprivileged LXC with nesting enabled.

### Docker Services

- Radarr
- Sonarr
- Prowlarr
- Bazarr
- qBittorrent
- Seerr
- Kavita
- FlareSolverr

## Storage Sharing

The Proxmox host's HDD is mounted at:

```text
/mnt/hdd/media
```

It is then exposed to the containers according to their role:

```text
Proxmox HDD
└── /mnt/hdd/media
    │
    ├── LXC 100 → /media/storage
    ├── LXC 101 → /media
    └── LXC 102 → /media/storage
```

This allows Jellyfin, Samba, and the Docker services to work with the same underlying data.

## Resource Allocation

The three containers currently have a combined allocation of:

- **5 CPU cores**
- **4.5 GB RAM**
- **68 GB root disk space**
- **1.5 GB swap**

The relatively small allocations are intentional because the Proxmox host has 8 GB of physical RAM.

## What This Demonstrates

This setup provides practical experience with:

- Proxmox LXC
- Unprivileged containers
- Resource allocation
- Static networking
- Bind mounts
- Shared storage
- GPU/device passthrough
- Linux permissions
- Docker inside LXC
- Service isolation
- Infrastructure troubleshooting
