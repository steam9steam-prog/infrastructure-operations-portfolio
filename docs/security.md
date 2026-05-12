# Безопасность

## Базовые правила

- секреты не коммитить
- SSH только по ключам
- наружу открывать только нужные порты
- админку и Grafana ограничивать
- webhook проверять по секрету, если возможно
- backup хранить не в публичной директории

## Что нельзя выкладывать

- .env
- Telegram bot token
- database password
- payment provider secrets
- API/webhook secrets
- реальные IP и домены, если они приватные
- дампы PostgreSQL

## Firewall

Базовый пример:

    sudo ufw allow OpenSSH
    sudo ufw allow 80/tcp
    sudo ufw allow 443/tcp
    sudo ufw enable

## Админка и мониторинг

Для админки, Prometheus и Grafana лучше использовать:

- allowlist IP
- basic auth
- VPN-only доступ
- закрытый internal port без публикации наружу

## Backup

Backup должен быть:

- регулярным
- доступным для восстановления
- не публичным
- проверенным через restore хотя бы на тестовой базе
