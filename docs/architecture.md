# Architecture

## Overview

The project runs as a live VPS-based service. The server hosts several components behind nginx:

- Website frontend
- Telegram mini app
- Telegram bot webhook
- Admin panel
- Internal API/control service
- PostgreSQL database
- Metrics endpoint for Prometheus
- Grafana dashboard

## High-Level Flow

    User Browser / Telegram
            |
            v
    DNS provider
            |
            v
    nginx reverse proxy + SSL
            |
            +--> website frontend
            +--> mini app frontend
            +--> bot webhook/API service
            +--> admin panel
            +--> Grafana, restricted

## Service Boundaries

The stack is split into externally exposed and internal services.

Externally exposed:

- Website
- Telegram mini app
- Telegram bot webhook
- Public API endpoints required by the product

Internal or restricted:

- PostgreSQL
- Prometheus
- Grafana
- Admin panel
- Internal maintenance endpoints

## Runtime Model

Two common runtime models are supported:

- Docker Compose for services that are easier to deploy as containers
- systemd for long-running host-level services or Python/Node workers

The exact choice depends on the project component. The main rule is that every long-running process must have a clear restart command, logs, environment configuration, and health check path.

## Domains And Routing

Example domain layout:

    example.com              -> website
    app.example.com          -> Telegram mini app
    api.example.com          -> API and bot webhook
    admin.example.com        -> admin panel, restricted
    grafana.example.com      -> Grafana, restricted

## Data Storage

PostgreSQL stores application data. Backups can be created with pg_dump and stored outside the application directory. Important backup changes should be checked with a test restore before relying on them.

## Observability

Operational visibility comes from:

- systemd service state
- journalctl logs
- nginx access and error logs
- application logs
- Prometheus metrics
- Grafana dashboards
- HTTP health checks
