# Proxmox Homelab

A personal homelab project built with **Proxmox VE** on a Dell OptiPlex 3020 MT.

The project is used to practice Linux system administration, virtualization, networking, storage management, Docker, and self-hosted service deployment.

## Hardware

| Component | Specification |
|---|---|
| System | Dell OptiPlex 3020 MT |
| CPU | Intel Core i5-4590 |
| RAM | 8 GB DDR3 |
| Proxmox OS | 120 GB SSD |
| Data storage | 500 GB HDD |

## Infrastructure

The host runs Proxmox VE with three Ubuntu LXC containers:

```text
Dell OptiPlex 3020 MT
└── Proxmox VE
    ├── LXC 100 — media
    │   └── Jellyfin
    │
    ├── LXC 101 — File-Server
    │   └── Samba
    │
    └── LXC 102 — Docker-arr-stack
        ├── Radarr
        ├── Sonarr
        ├── Prowlarr
        ├── Bazarr
        ├── qBittorrent
        ├── Seerr
        ├── Kavita
        └── FlareSolverr
```

## Services

The homelab currently provides:

- **Jellyfin** — media streaming
- **Samba** — network file sharing
- **Sonarr** — TV series management
- **Radarr** — movie management
- **Prowlarr** — indexer management
- **Bazarr** — subtitle management
- **qBittorrent** — download management
- **Seerr** — media requests
- **Kavita** — books, comics and manga
- **FlareSolverr** — supporting service for compatible indexers

## Networking

The homelab uses a private LAN with Proxmox virtual networking through `vmbr0`.

Remote access is provided through **Tailscale** rather than exposing services directly to the public Internet.

No public IPs, Tailscale addresses, credentials, or API keys are included in this documentation.

## Storage

The 500 GB HDD is used for the main homelab data and media storage.

The storage is shared with the relevant LXC containers through Proxmox mount points, allowing multiple services to work with the same data.

## Documentation

Detailed documentation is available here:

- [Proxmox](docs/proxmox.md) — host hardware, virtualization and storage
- [Networking](docs/networking.md) — network architecture and remote access
- [Containers](docs/containers.md) — LXC configuration and resource allocation
- [Services](docs/services.md) — deployed services and Docker stack

## Screenshots

Screenshots of the homelab are available in the [images](images/) directory.

## What I Learned

This project has given me hands-on experience with:

- Linux system administration
- Proxmox VE and LXC
- Docker
- Networking and virtual bridges
- Storage and mount points
- Permissions and ownership
- Hardware/device passthrough
- Service deployment
- Troubleshooting
- Self-hosted infrastructure

## Project Status

This homelab is an ongoing project. The infrastructure and services evolve as I learn and add new technologies.
