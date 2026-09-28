# Homelab

A self-hosted homelab built on an old laptop running Debian 13, managed with Docker.

## Stack

| Service | Purpose |
|---|---|
| Traefik | Reverse proxy, routes traffic by domain name |
| Portainer | Docker container management UI |
| Prometheus + Grafana | Monitoring and metrics dashboard |
| Node Exporter | Host metrics collector |
| Pi-hole | Network-wide ad blocker and DNS server |
| Minecraft (PaperMC) | Self-hosted game server |
| Playit.gg | Tunnel for external access without port forwarding |

## Architecture

- All services run in Docker containers
- Traefik handles routing via local domains (portainer.local, grafana.local etc)
- Pi-hole acts as DNS server for all devices on the network
- Monitoring via Prometheus scraping Node Exporter, visualized in Grafana

## Services

### Traefik
Reverse proxy that automatically detects Docker containers via labels and routes traffic.

### Prometheus + Grafana
Full monitoring stack. Grafana dashboard shows real-time CPU, RAM, disk and network usage of the host machine.

### Pi-hole
Network-wide DNS-based ad blocker. Blocks 76,000+ ad domains out of the box.

### Minecraft Server
PaperMC 1.21.1 server running in Docker with persistent world data and automatic restarts.

## Setup Notes

Each service has its own `docker-compose.yml`. Services are connected via a shared Docker network (`traefik_default`) so Traefik can route to all of them.

Sensitive values like passwords and API keys are kept in `.env` files (not committed). See `.env.example` for required variables.

