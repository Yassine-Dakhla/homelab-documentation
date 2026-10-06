# Services

The homelab hosts several services for media management, file sharing, and self-hosted applications.

## Service List

| Service | Purpose |
|---|---|
| Jellyfin | Media streaming |
| Samba | Network file sharing |
| Sonarr | TV series management |
| Radarr | Movie management |
| Prowlarr | Indexer management |
| Bazarr | Subtitle management |
| Seerr | Media request management |
| Kavita | Books, comics and manga |
| Docker | Application container runtime |

## Media Storage

The main media/data storage is located on the 500 GB HDD.

The storage is mounted into relevant containers so applications can access the same underlying media without duplicating the files.

## Containerization

The lab uses both:

- **LXC** for lightweight system services
- **Docker** where an application is better suited to containerized deployment

This gives the project practical experience with two different containerization approaches.

## What This Teaches

Running these services provides hands-on experience with:

- Linux administration
- Service configuration
- Permissions and ownership
- Storage mounts
- Networking
- Docker
- LXC
- Application troubleshooting
- Media automation
