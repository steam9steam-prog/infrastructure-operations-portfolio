# VPN Infrastructure Case Study

Infrastructure case study for a live VPS-based VPN service.

This repository does not contain private application code, secrets, real domains, IP addresses, tokens, database dumps, or real server configuration files. It shows the operational approach, deployment model, monitoring practices, and incident handling process for a live service.

## Role

Middle Infrastructure / Operations Engineer

## Service Scope

The service includes:

- Public website
- Telegram bot
- Telegram mini app
- Admin panel
- VPN control service
- PostgreSQL database
- Grafana dashboards and metrics
- Systemd-managed services
- nginx reverse proxy with SSL

## Infrastructure Stack

- VPS Linux server
- Docker and Docker Compose
- nginx reverse proxy
- Let's Encrypt SSL certificates
- PostgreSQL
- systemd
- Prometheus and Grafana
- journalctl and application logs
- Basic backup and restore workflow
- Firewall and SSH key access

## What This Case Study Shows

- How a live service can be structured on a VPS
- How services are deployed and restarted safely
- How nginx routes website, API, bot webhook, and admin traffic
- How logs and metrics are used for diagnostics
- How incidents are investigated with a repeatable runbook
- How secrets are kept out of public repositories

## What You Can Review

- Architecture and routing notes
- Docker Compose and systemd deployment flow
- nginx example for API/webhook and HTTPS
- systemd service example
- Docker Compose example
- Monitoring and alerting notes
- Incident runbook

## Repository Structure

    README.md
    README.en.md
    docs/architecture.md
    docs/deployment.md
    docs/monitoring.md
    docs/security.md
    docs/incident-runbook.md
    docs-en/architecture.md
    docs-en/deployment.md
    docs-en/monitoring.md
    docs-en/security.md
    docs-en/incident-runbook.md
    examples/nginx/example.conf
    examples/systemd/example.service
    examples/docker-compose/docker-compose.example.yml
    examples/prometheus/alerts.example.yml

Russian documentation is in docs/. English documentation is in docs-en/.

## Operational Responsibilities

- Deploy application updates
- Restart and inspect services
- Configure nginx and SSL
- Check logs after incidents
- Monitor health metrics
- Maintain PostgreSQL backups
- Keep systemd services stable
- Diagnose webhook, API, and connectivity issues

## Safety Notes

All examples use placeholder values:

- example.com
- 127.0.0.1
- CHANGE_ME
- placeholder service names
- placeholder ports

Service secrets should be stored in server-side .env files or host-level environment variables and must never be committed.
