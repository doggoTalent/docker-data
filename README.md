# Docker monitoring stack

Production-ready monitoring suite with Grafana, Prometheus, Node Exporter, and a static landing page.

## Services

| Service        | Description                         | Internal port       | Public endpoint                    |
|----------------|-------------------------------------|---------------------|------------------------------------|
| landing        | Static landing page (portfolio)     | 8000                | `https://doggotalent.xyz`          |
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

## Requirements

- Docker Engine ≥ 20.10
- Docker Compose ≥ 2.0
