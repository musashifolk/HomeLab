# Homelab

A self-hosted homelab built on an old laptop running Debian 13, managed with Docker.

## Stack

| Logo | Name | Description |
|------|------|-------------|
| <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg" width="32"/> | [Docker](https://docker.com) | Container runtime for all services |
| <img src="https://raw.githubusercontent.com/traefik/traefik/master/docs/content/assets/img/traefik.logo.png" width="32"/> | [Traefik](https://traefik.io) | Reverse proxy that routes traffic by domain name |
| <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/prometheus/prometheus-original.svg" width="32"/> | [Prometheus](https://prometheus.io) | Metrics collection and storage |
| <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/grafana/grafana-original.svg" width="32"/> | [Grafana](https://grafana.com) | Visualization and dashboards |
| <img src="https://raw.githubusercontent.com/pi-hole/AdminLTE/master/img/logo.svg" width="32"/> | [Pi-hole](https://pi-hole.net) | Network-wide DNS ad blocker |
| <img src="https://raw.githubusercontent.com/louislam/uptime-kuma/master/public/icon.svg" width="32"/> | [Uptime Kuma](https://github.com/louislam/uptime-kuma) | Service uptime monitoring |
| <img src="https://raw.githubusercontent.com/portainer/portainer/develop/app/assets/images/logo_alt.svg" width="32"/> | [Portainer](https://portainer.io) | Docker container management UI |

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

