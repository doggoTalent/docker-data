# Docker containers and network configuration

Monitoring suite with Grafana, Prometheus, Node Exporter, and a static landing page.

## Services

| Service        | Description                         | Internal port       | Public endpoint                    |
|----------------|-------------------------------------|---------------------|------------------------------------|
| landing        | Static landing page                 | 8000                | `https://doggotalent.xyz`          |
| prometheus     | Metrics collection & storage        | 9090                | (internal only)                    |
| grafana        | Dashboards & visualisation          | 3000                | `https://doggotalent.xyz/grafana/` |
| node_exporter  | Host system metrics (CPU, RAM, etc) | 9100                | (internal only)                    |

## Features

- **Persistence** – Prometheus & Grafana data stored in Docker named volumes (`prometheus_data`, `grafana_data`).
- **Anonymous Grafana access** – any visitor can view dashboards without login.
- **Auto‑provisioning** – Grafana comes with:
  - Prometheus datasource pre‑configured.
  - Node Exporter Full dashboard (ID 1860) pre‑loaded.
- **Submodule** – Landing page source lives in [`doggoTalent/landing`](https://github.com/doggoTalent/landing) (linked as `projects/landing`).

## Files
.
├── projects.
│   └── landing
│       ├── Dockerfile                        # Image for landing container
│       └── ... 
├── volumes
│   ├── grafana
│   │   ├── config
│   │   │   └── grafana.ini                    # Grafana main config file
│   │   └── provisioning
│   │       ├── dashboards
│   │       │   ├── dashboards.yml             # Grafana config for managing dashboards
│   │       │   └── node_exporter_full.json    # Grafana dashboard preset 
│   │       └── datasources
│   │           └── prometheus.yml             # Grafana config for managing datasources
│   └── prometheus
│       └── config
│           └── prometheus.yml                 # Prometheus main config file
├── README.md
├── docker-compose.yml                         **# Main orchestration file**
├── test.sh
└── update-landing.sh                          # Semi-automated script for updating container: git pull, rebuild, and restart container 

## Requirements

- Docker Engine ≥ 20.10
- Docker Compose ≥ 2.0
