# Docker containers and network configuration

Monitoring suite with Grafana, Prometheus, Alertmanager, Node Exporter, and a static landing page.

## Services

| Service        | Description                         | Internal port       | Public endpoint                    |
|----------------|-------------------------------------|---------------------|------------------------------------|
| landing        | Static landing page                 | 8000                | `https://doggotalent.xyz`          |
| grafana        | Dashboards & visualisation          | 3000                | `https://doggotalent.xyz/grafana/` |
| prometheus     | Metrics collection & storage        | 9090                | (internal only)                    |
| alertmanager   | Alert routing (Telegram)            | 9093                | (internal only)                    |
| node_exporter  | Host system metrics (CPU, RAM, etc) | 9100                | (internal only)                    |

## Features

- **Persistence** – Prometheus & Grafana data stored in Docker named volumes (`prometheus_data`, `grafana_data`, `alertmanager-data`).
- **Anonymous Grafana access** – any visitor can view dashboards without login.
- **Auto‑provisioning** – Grafana comes with:
  - Prometheus datasource pre‑configured.
  - Node Exporter Full dashboard (ID 1860) pre‑loaded.
- **Alerting** – Prometheus native alert rules (CPU load, memory, disk, etc.) are evaluated. Firing alerts are sent to Alertmanager, which forwards them to **Telegram** (credentials stored outside the repo).
- **Secrets management** – Sensitive files (`alertmanager.yml`, any `.env`) are **excluded** from version control (see `.gitignore`). A template (`alertmanager.tmpl.yml`) is provided.
- **Submodule** – Landing page source lives in [`doggoTalent/landing`](https://github.com/doggoTalent/landing) (linked as `projects/landing`).

## File structure

```text
.
├── projects
│   └── landing
│       ├── Dockerfile
│       ├── index.html
│       └── ...                (submodule content)
├── volumes
│   ├── alertmanager
│   │   ├── alertmanager.tmpl.yml   # template – commit this
│   │   └── alertmanager.yml        # real config (secrets) – ignored by Git
│   ├── grafana
│   │   ├── grafana.ini              # ignored (may contain secrets)
│   │   └── provisioning
│   │       ├── dashboards
│   │       │   ├── dashboards.yml
│   │       │   └── node_exporter_full.json
│   │       └── datasources
│   │           └── prometheus.yml
│   └── prometheus
│       ├── alerts
│       │   └── node_alerts.yml
│       └── prometheus.yml
├── .gitignore
├── .gitmodules
├── README.md
├── docker-compose.yml
├── auto_updater_landing.sh
├── test.sh
└── update-landing.sh
