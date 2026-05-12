# Incident Runbook

## Первые действия

Когда что-то упало:

1. Проверить, проблема у всех или у одного пользователя.
2. Понять, упал весь сервер или один сервис.
3. Вспомнить последние изменения: деплой, nginx, SSL, база, домен.
4. Посмотреть статус сервисов.
5. Посмотреть свежие логи.
6. Решить: рестарт, откат или deeper debug.

## Базовая проверка сервера

    uptime
    df -h
    free -m
    sudo systemctl status nginx --no-pager
    sudo nginx -t
    docker compose ps

## Если упал systemd service

    sudo systemctl status example-api.service --no-pager
    journalctl -u example-api.service -n 200 --no-pager
    sudo systemctl restart example-api.service
    journalctl -u example-api.service -f

Частые причины:

- нет переменной окружения
- сломался deploy
- порт занят
- база недоступна
- ошибка прав
- сервис уходит в restart loop

## Если проблема в nginx

    sudo nginx -t
    sudo systemctl status nginx --no-pager
    sudo tail -n 100 /var/log/nginx/error.log
    sudo systemctl reload nginx

Проверить:

- правильный upstream port
- жив ли backend
- выпущен ли SSL
- верные ли WebSocket headers
- DNS смотрит на нужный сервер

## Если проблема с базой

    sudo systemctl status postgresql --no-pager
    sudo -u postgres psql -c "select now();"

Проверить:

- место на диске
- подключения
- логин/пароль
- миграции
- последний backup

## После починки

Коротко записать:

    Дата:
    Что сломалось:
    Как заметили:
    Причина:
    Что сделали:
    Как не повторить:
