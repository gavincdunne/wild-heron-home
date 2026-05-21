# Wild Heron Home
*Built by WeekendWare*

> A self-hosted home built on open source. Media, smart home, automation, and whatever else sounds fun.

Named for Wild Heron Road on Saint Simons Island, Georgia.

---

## What is this?

A repurposed gaming PC — Ryzen 5 3600, RTX 2060, 32GB RAM — turned into a full home server running
open source software. Media streaming, smart home automation, self-hosted photo backup, network-wide
ad blocking, game streaming, and a growing collection of edge automation projects.

Everything runs as Docker containers. Zero subscriptions, zero cloud dependency.
The machine was already here — it just needed a better job.

---

## Architecture

```
  ┌──────────────────────────────────────────────────────────────────┐
  │                  Wild Heron Home — Main PC                       │
  │              Ryzen 5 3600  ·  RTX 2060  ·  32GB RAM             │
  │                                                                  │
  │  ┌────────────┐  ┌────────────┐  ┌───────────────────────────┐  │
  │  │  Jellyfin  │  │   Immich   │  │      Home Assistant       │  │
  │  │  movies &  │  │   photos   │  │     smart home brain      │  │
  │  │     TV     │  │  & videos  │  │                           │  │
  │  └────────────┘  └────────────┘  └─────────────┬─────────────┘  │
  │                                                 │                │
  │  ┌────────────┐  ┌────────────┐                 │                │
  │  │  Pi-hole   │  │  Sunshine  │                 │                │
  │  │  DNS / ads │  │   gaming   │                 │                │
  │  └────────────┘  └────────────┘                 │                │
  │                                                 │                │
  │  ┌────────────┐  ┌────────────┐                 │                │
  │  │  Portainer │  │ Tailscale  │                 │                │
  │  │ containers │  │    VPN     │                 │                │
  │  └────────────┘  └────────────┘                 │                │
  └─────────────────────────────────────────────────┼────────────────┘
                                                    │
                    ┌───────────────────────────────┘
                    │
        ┌───────────┼──────────────────────┐
        │           │                      │
        ▼           ▼                      ▼
  ┌──────────┐  ┌──────────┐      ┌─────────────────┐
  │  Pi Dog  │  │  Gaggia  │      │  Smart Devices  │
  │  Feeder  │  │ Espresso │      │ lights · locks  │
  │  Max 🐾  │  │  ☕       │      │ cameras · more  │
  └──────────┘  └──────────┘      └─────────────────┘

  Clients:  Smart TV  ·  MacBook Air  ·  Phone  ·  anywhere via Tailscale
```

---

## The Stack

| Service | What it does |
|---|---|
| [Jellyfin](https://jellyfin.org) | Streams local movies and TV to any device — personal Netflix, zero subscription |
| [Immich](https://immich.app) | Automatic phone photo backup — self-hosted Google Photos |
| [Pi-hole](https://pi-hole.net) | Blocks ads and tracking at the DNS level for every device on the network |
| [Home Assistant](https://home-assistant.io) | The smart home brain — connects everything, automates everything |
| [Portainer](https://portainer.io) | Browser UI for managing all running containers |
| [Sunshine](https://app.lizardbyte.dev/Sunshine) | Streams games from this PC to the TV or MacBook via the GPU |
| [Tailscale](https://tailscale.com) | VPN that just works — reach everything at home from anywhere |

---

## Roadmap

### Done
- [x] Stack designed and containerized
- [x] Repository scaffolded with docs and architecture
- [x] SSH and GitHub workflow established

### In Progress
- [ ] First container launch and service validation
- [ ] Pi-hole as network DNS
- [ ] Tailscale remote access setup

### Coming Up
- [ ] Smart lights via Zigbee2MQTT
- [ ] Home Assistant automations (lighting scenes, routines)
- [ ] Immich mobile setup and photo migration off Google
- [ ] Sunshine game streaming to the TV
- [ ] Network segmentation — IoT devices on their own VLAN
- [ ] Frigate NVR for security cameras with AI object detection
- [ ] Backup strategy (3-2-1: local + offsite + cloud)
- [ ] Monitoring dashboard (Grafana + Prometheus)
- [ ] Ansible playbook — fully reproducible setup from scratch

---

## Edge Projects

These live in their own repos and talk back to the main stack through Home Assistant.

| Project | What it does |
|---|---|
| [`pi-dog-feeder`](https://github.com/gavincdunne/pi-dog-feeder) | Raspberry Pi automated feeder for Max — scheduled or triggered from your phone |
| [`gaggia-automation`](https://github.com/gavincdunne/gaggia-automation) | Wake up to a pre-made espresso. The Gaggia starts itself. |

---

## Getting Started

```bash
git clone git@github.com:gavincdunne/wild-heron-home.git
cd wild-heron-home

cp .env.example .env
# Fill in your paths and passwords

docker compose up -d
docker compose ps
```

---

*Built with Docker, Home Assistant, and an unreasonable amount of coffee.*
