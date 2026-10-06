# Proxmox VE

## Overview

This homelab runs Proxmox VE on a Dell OptiPlex 3020 MT. The goal is to learn virtualization, Linux system administration, networking, storage management, and service deployment using real infrastructure.

## Host Hardware

| Component | Specification |
|---|---|
| System | Dell OptiPlex 3020 MT |
| CPU | Intel Core i5-4590 |
| RAM | 8 GB DDR3 |
| Proxmox OS disk | 120 GB SSD |
| Data disk | 500 GB HDD |

## Virtualization

The host uses both **LXC containers** and **virtual machines**.

LXC containers are preferred for lightweight Linux services because they use fewer resources. Virtual machines are used when full hardware or operating-system isolation is useful.

## Storage

The system separates the Proxmox installation from bulk media/data storage:

- 120 GB SSD — Proxmox/system storage
- 500 GB HDD — homelab data and media storage

## Current Approach

The lab is intentionally built with limited hardware. Services are added gradually and resources are kept small so the system remains practical on 8 GB of RAM.

This project is also a learning environment: configurations are tested, problems are documented, and services are adjusted as the lab evolves.
