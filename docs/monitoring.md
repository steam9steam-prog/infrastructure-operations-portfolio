# Monitoring

## Goals

Monitoring should answer three practical questions:

- Is the service up?
- Is it serving users correctly?
- What changed before the incident?

## Signals

Minimum useful signals:

- HTTP health status
- API request count
- API error count
- Bot webhook failures
- Queue or background job failures
- Database availability
- Disk usage
- Memory usage
- Service restarts
- SSL certificate expiry

## Prometheus Targets

Example targets:

    api: metrics endpoint
    node_exporter: host metrics
    postgres_exporter: database metrics
    nginx exporter or log-derived metrics

## Grafana Dashboards

Useful panels:

- Service uptime
- Request rate
- Error rate
- Response latency
- CPU and memory
- Disk usage
- PostgreSQL connections
- Background job failures
- Business events, if available

## Alert Rules

Alerts should be clear and actionable:

- Service down
- High error rate
- Disk almost full
- Database unavailable
- SSL certificate close to expiry
- No successful bot events for an unusual period

## Log Sources

    journalctl -u example-api.service -f
    sudo tail -f /var/log/nginx/access.log
    sudo tail -f /var/log/nginx/error.log
    docker compose logs -f api

## Incident Notes

Every incident should leave an incident note:

- What happened
- When it started
- How it was detected
- What fixed it
- What should be improved
