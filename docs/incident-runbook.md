# Incident Runbook

## First 5 Minutes

1. Confirm the issue.
2. Check whether the whole server is down or only one service.
3. Check recent deploys or config changes.
4. Check service status and logs.
5. Decide whether to rollback, restart, or investigate deeper.

## Basic Commands

    uptime
    df -h
    free -m
    sudo systemctl status nginx --no-pager
    sudo nginx -t
    docker compose ps

## systemd Service Down

    sudo systemctl status example-api.service --no-pager
    journalctl -u example-api.service -n 200 --no-pager
    sudo systemctl restart example-api.service
    journalctl -u example-api.service -f

Check:

- Missing environment variable
- Broken dependency
- Database unavailable
- Port already in use
- Permission problem
- Bad deploy

## nginx Routing Problem

    sudo nginx -t
    sudo systemctl status nginx --no-pager
    sudo tail -n 100 /var/log/nginx/error.log
    sudo systemctl reload nginx

Check:

- Wrong upstream port
- Service not listening
- SSL certificate issue
- WebSocket headers missing
- DNS points to wrong IP

## Database Problem

    sudo systemctl status postgresql --no-pager
    sudo -u postgres psql -c "select now();"

Check:

- Disk full
- Too many connections
- Wrong credentials
- Migration failed
- Backup restore needed

## Telegram Bot/Webhook Problem

Check:

- Webhook URL uses HTTPS
- nginx routes to the right service
- Bot token is correct
- App logs show incoming requests
- Telegram API returns a useful error

## After Fix

Write an incident note:

    Date:
    Impact:
    Root cause:
    Fix:
    Prevention:
