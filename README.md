# Kittygram

[![Main Kittygram workflow](https://github.com/Stepan-Pimenov/kittygram_final/actions/workflows/main.yml/badge.svg)](https://github.com/Stepan-Pimenov/kittygram_final/actions/workflows/main.yml)

Kittygram - социальная сеть для обмена фотографиями котиков. Пользователь
регистрируется, добавляет своих котов с фото и описанием, отмечает их
достижения и смотрит ленту котиков других пользователей.

## Возможности

- Регистрация и авторизация по токену.
- Добавление котика: имя, цвет, год рождения, достижения, фотография.
- Просмотр ленты котиков с постраничной навигацией.
- Редактирование и удаление своих котиков.

## Стек

- Python, Django, Django REST Framework, Djoser
- PostgreSQL
- React
- Nginx, Docker, Docker Compose
- GitHub Actions (CI/CD)

## Как развернуть проект локально

1. Клонировать репозиторий:
   ```bash
   git clone git@github.com:Stepan-Pimenov/kittygram_final.git
   cd kittygram_final
   ```
2. Создать в корне файл `.env` (пример переменных - в `.env.example`).
3. Собрать и запустить контейнеры:
   ```bash
   docker compose up -d
   ```
4. Применить миграции и собрать статику:
   ```bash
   docker compose exec backend python manage.py migrate
   docker compose exec backend python manage.py collectstatic
   docker compose exec backend cp -r /app/collected_static/. /backend_static/static/
   ```

Проект будет доступен по адресу http://localhost:9000/

## Как заполнить .env

```
POSTGRES_DB=имя_базы
POSTGRES_USER=имя_пользователя_базы
POSTGRES_PASSWORD=пароль_базы
DB_HOST=db
DB_PORT=5432
SECRET_KEY=секретный_ключ_django
DEBUG=False
ALLOWED_HOSTS=домен,ip,localhost,127.0.0.1
```

Если нужно быстро протестировать проект на SQLite вместо PostgreSQL,
добавьте переменную `USE_SQLITE=True`.

## CI/CD

При пуше в ветку `main` GitHub Actions запускает тесты, собирает образы,
отправляет их на Docker Hub, обновляет контейнеры на сервере и присылает
уведомление в Telegram. Тесты запускаются при пуше в любую ветку.

## Автор

Степан Пименов, [Stepan-Pimenov](https://github.com/Stepan-Pimenov)
