# Deployment

## Goal

Deploy Telegram, mini app, VPN, or web services to a VPS in a repeatable and recoverable way.

## Pre-Deployment Checklist

- SSH access works with keys
- Domain DNS points to the server
- Firewall allows only required ports
- .env exists on the server and is not committed
- nginx config is valid
- SSL certificate is issued
- Database migrations or schema changes are understood
- Backup exists before risky changes

## Typical Docker Compose Deployment

    ssh deploy@example.com
    cd /opt/example-service
    git pull
    docker compose pull
    docker compose up -d --build
    docker compose ps
    docker compose logs --tail=100 api

## Typical systemd Deployment

    ssh deploy@example.com
    cd /opt/example-service
    git pull
    sudo systemctl daemon-reload
    sudo systemctl restart example-api.service
    sudo systemctl status example-api.service --no-pager
    journalctl -u example-api.service -n 100 --no-pager

## nginx Validation

    sudo nginx -t
    sudo systemctl reload nginx
    sudo systemctl status nginx --no-pager

## Post-Deployment Checks

- Website opens over HTTPS
- Bot webhook returns expected status
- Mini app loads inside Telegram
- Admin panel is reachable only from allowed sources
- API health endpoint returns 200
- Logs do not show repeated exceptions
- Prometheus target is up
- Grafana dashboard receives fresh data

## Rollback Approach

For VPS services, rollback should be clear:

- Keep previous Git commit known
- Keep previous Docker image tag if available
- Keep database backup before migrations
- Avoid destructive migrations without a tested rollback
- Revert nginx changes if routing breaks
