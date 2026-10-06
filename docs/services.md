# Services

The homelab runs a mix of native Linux services and Docker containers for media streaming, file sharing, media automation, and digital library management.

## Architecture

The current deployment is organized into three LXC containers:

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
        ├── Prowlarr
        ├── Sonarr
        ├── Bazarr
        ├── qBittorrent
        ├── Seerr
        ├── Kavita
        └── FlareSolverr
```

## Service Layout

| LXC | Service | Deployment | Purpose |
|---|---|---|---|
| 100 | Jellyfin | Native Linux service | Media streaming |
| 101 | Samba | Native Linux service | Network file sharing |
| 102 | Radarr | Docker | Movie management |
| 102 | Prowlarr | Docker | Indexer management |
| 102 | Sonarr | Docker | TV series management |
| 102 | Bazarr | Docker | Subtitle management |
| 102 | qBittorrent | Docker | Download management |
| 102 | Seerr | Docker | Media request management |
| 102 | Kavita | Docker | Books, comics and manga |
| 102 | FlareSolverr | Docker | Web challenge handling for supported indexers |

## Service Ports

| Service | Port |
|---|---:|
| Jellyfin | 8096 |
| Samba | 139 / 445 |
| qBittorrent | 8080 |
| Kavita | 5000 |
| Seerr | 5055 |
| Bazarr | 6767 |
| Prowlarr | 9696 |
| Radarr | 7878 |
| Sonarr | 8989 |
| FlareSolverr | 8191 |

## Storage

The main data storage is provided by the 500 GB HDD attached to the Proxmox host.

The storage is mounted into the relevant LXC containers, allowing multiple services to work with the same media and data without unnecessary duplication.

## Containerization

The lab uses two levels of containerization:

- **LXC** for separating Linux services from the Proxmox host
- **Docker** inside LXC 102 for the media automation stack

This setup provides practical experience with Linux administration, LXC, Docker, networking, storage mounts, permissions, and service troubleshooting.

## Current Service Stack

The current stack focuses on a simple media workflow:

```text
Seerr
  │
  ├── Requests
  │
  ▼
Sonarr / Radarr
  │
  ├── Indexers
  │      └── Prowlarr
  │
  ├── Downloads
  │      └── qBittorrent
  │
  └── Subtitles
         └── Bazarr

Media Storage
  ├── Jellyfin
  └── Kavita
```

FlareSolverr is available as a supporting service for compatible indexers.

## What This Teaches

Running these services provides hands-on experience with:

- Linux system administration
- Proxmox LXC
- Docker
- Service deployment
- Networking
- Storage mounts
- Permissions and ownership
- Media automation
- Troubleshooting
