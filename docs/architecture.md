# Architecture

## System Overview

```
  ┌──────────────────────────────────────────────────────────────────────────┐
  │                      Wild Heron Home — Main PC                           │
  │                  Ryzen 5 3600  ·  RTX 2060  ·  32GB RAM                 │
  │                                                                          │
  │   Jellyfin        — media streaming (movies, TV)           port 8096     │
  │   Immich          — photo & video backup                   port 2283     │
  │   Home Assistant  — smart home automation brain            port 8123     │
  │   Pi-hole         — DNS-level ad & tracker blocking        port 8080     │
  │   Portainer       — Docker container management UI         port 9443     │
  │   Sunshine        — GPU game streaming (NVENC)             port 47990    │
  │   Tailscale       — zero-config remote access VPN          —             │
  │                                                                          │
  └──────────┬───────────────────────────────┬───────────────────────────────┘
             │                               │
             │  Home Assistant controls      │  Pi-hole handles
             │  all edge devices via         │  DNS for the whole
             │  MQTT / ESPHome / Zigbee      │  home network
             │                               │
    ┌────────┼──────────────────┐     ┌──────┴────────────┐
    │        │                  │     │   Home Network    │
    ▼        ▼                  ▼     │   Router          │
┌────────┐ ┌──────────┐ ┌──────────┐ └───────────────────┘
│  Pi    │ │  Gaggia  │ │  Zigbee  │
│  Dog   │ │  Brew    │ │  Lights  │
│ Feeder │ │  (ESP32) │ │  Locks   │
│ (MQTT) │ │          │ │  Cameras │
└────────┘ └──────────┘ └──────────┘

  Clients
  ───────
  Smart TV      ←  Jellyfin (media)  ·  Sunshine (game stream)
  MacBook Air   ←  Jellyfin (media)  ·  Sunshine (game stream)  ·  Tailscale (remote)
  Phone         ←  Immich (photos)   ·  Tailscale (remote)
```

---

## Services

| Service | Role | Port |
|---|---|---|
| Home Assistant | Smart home brain — automation, integrations, dashboards | 8123 |
| Jellyfin | Media streaming — movies and TV to any device | 8096 |
| Immich | Photo and video backup — self-hosted Google Photos | 2283 |
| Pi-hole | DNS-level ad blocking for the whole network | 8080 |
| Portainer | Docker container management UI | 9443 |
| Sunshine | GPU-accelerated game streaming via NVENC | 47990 |
| Tailscale | Zero-config VPN for remote access from anywhere | — |

---

## Edge Nodes

| Node | Hardware | How it connects |
|---|---|---|
| Dog feeder | Raspberry Pi + servo motor | Home Assistant via MQTT |
| Espresso machine | Gaggia + ESP32 / smart plug | Home Assistant schedule |
| Lighting | Zigbee bulbs and switches | Home Assistant via Zigbee2MQTT |
| Door locks | Z-Wave or Matter devices | Home Assistant integration |
| Security cameras | IP cameras | Home Assistant + Frigate NVR |

---

## Skills Demonstrated

- **Docker / Docker Compose** — multi-service containerized stack
- **Networking** — DNS, DHCP, VLANs, firewall rules
- **Linux administration** — WSL2, service management, shell scripting
- **IoT / embedded** — MQTT, ESPHome, Zigbee2MQTT, Raspberry Pi GPIO
- **Infrastructure as code** — declarative Compose files, environment-based config
- **Home automation** — event-driven logic, API integrations, webhooks
