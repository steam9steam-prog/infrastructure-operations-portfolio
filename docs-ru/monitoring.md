# Мониторинг

## Задача мониторинга

Мониторинг нужен не для красоты. Он должен быстро отвечать:

- сервис живой?
- пользователи могут им пользоваться?
- что сломалось первым?

## Минимум, который полезен

- health endpoint
- доступность API
- количество ошибок
- рестарты systemd/Docker
- свободное место на диске
- CPU/RAM
- доступность PostgreSQL
- срок действия SSL
- ошибки webhook бота

## Что смотреть в Grafana

- uptime
- request rate
- error rate
- latency
- CPU/RAM
- disk usage
- PostgreSQL connections
- bot/webhook events

## Логи

Самые частые команды:

    journalctl -u example-api.service -f
    journalctl -u example-api.service -n 200 --no-pager
    sudo tail -f /var/log/nginx/error.log
    sudo tail -f /var/log/nginx/access.log
    docker compose logs -f api

## Алерты

Алертов не должно быть слишком много. Лучше несколько понятных:

- сервис упал
- много 5xx ошибок
- диск почти заполнен
- база недоступна
- SSL скоро истечет
- бот долго не получает успешных событий
