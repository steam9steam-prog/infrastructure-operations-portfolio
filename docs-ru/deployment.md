# Деплой

## Цель

Деплой должен быть повторяемым: понятно, какие команды запускать, где смотреть ошибки и как проверить, что сервис живой.

## Перед деплоем

Проверяю:

- SSH-доступ работает
- домен смотрит на сервер
- .env есть на сервере
- секреты не лежат в Git
- nginx config проходит проверку
- SSL выпущен
- есть свежий backup, если изменение рискованное

## Docker Compose вариант

    ssh deploy@example.com
    cd /opt/example-service
    git pull
    docker compose up -d --build
    docker compose ps
    docker compose logs --tail=100 api

## systemd вариант

    ssh deploy@example.com
    cd /opt/example-service
    git pull
    sudo systemctl daemon-reload
    sudo systemctl restart example-api.service
    sudo systemctl status example-api.service --no-pager
    journalctl -u example-api.service -n 100 --no-pager

## nginx

    sudo nginx -t
    sudo systemctl reload nginx
    sudo systemctl status nginx --no-pager

## После деплоя

Проверяю:

- сайт открывается по HTTPS
- API health возвращает 200
- webhook бота отвечает
- mini app грузится
- в логах нет повторяющихся ошибок
- сервис не уходит в restart loop
- метрики в Grafana обновляются

## Откат

Для VPS-проекта откат должен быть понятным:

- знать предыдущий рабочий commit
- иметь backup базы перед рискованными изменениями
- уметь вернуть старый nginx config
- не делать необратимые миграции без плана
