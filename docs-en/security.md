# Security

## Principles

- Keep secrets out of Git
- Expose only required ports
- Use SSH keys instead of passwords
- Restrict admin and monitoring endpoints
- Validate webhooks with secrets
- Keep backups protected
- Stop startup when required secrets are missing

## Server Access

Recommended baseline:

    sudo ufw allow OpenSSH
    sudo ufw allow 80/tcp
    sudo ufw allow 443/tcp
    sudo ufw enable

SSH access should use keys. Password login should be disabled after key access is confirmed.

## Secrets

Do not commit:

- Telegram bot tokens
- Payment provider tokens
- Database passwords
- API keys
- API secrets
- Real .env files
- Real nginx configs with private hostnames if sensitive

Use .env.example to document required variables without real values.

## nginx Restrictions

Admin and monitoring routes should be protected with at least one of:

- IP allowlist
- Basic auth
- VPN-only access
- Internal network access

## Backups

Backups should be:

- Created automatically
- Stored outside the app directory
- Protected from public access
- Rotated
- Tested with restore commands

## Webhooks

Webhook endpoints should verify a secret header or token where supported. Unknown or invalid webhook calls should be rejected.
