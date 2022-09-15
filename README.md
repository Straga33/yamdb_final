# Проект YamDB для сбора отзывов пользователей на произведения.
![example workflow](https://github.com/Straga33/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

Проект YamDB собирает отзывы (Review) пользователей на произведения (Title). Произведения делятся на категории: "Книги", "Фильмы", "Музыка". Список категорий (Category) может быть расширен.
Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.

Сборка docker представляет из собой три образа: web, db, nginx. При создании контейнеров из образов, будет создано два тома для работы со статикой и медиа файлами. Название томов: static_value, media_value

web образ содержит сам проект, все зависимости, в том числе gunicorn server для корректной работы, документацию к API проекта YAMDB (v1.0)
nginx образ содержит веб сервер,
db образ содержит PostgresSQL базу данных проекта
Оркестрация контейнерами происходит по средствам docker-compose утилиты.

![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Nginx](https://img.shields.io/badge/nginx-%23009639.svg?style=for-the-badge&logo=nginx&logoColor=white)
![Gunicorn](https://img.shields.io/badge/gunicorn-%298729.svg?style=for-the-badge&logo=gunicorn&logoColor=white)
![DjangoREST](https://img.shields.io/badge/DJANGO-REST-ff1709?style=for-the-badge&logo=django&logoColor=white&color=ff1709&labelColor=gray)
![Django](https://img.shields.io/badge/django-%23092E20.svg?style=for-the-badge&logo=django&logoColor=white)
![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white)

## Стек технологий в проекте:
- Python
- Dajngo
- REST API
- PostgreSQL
- nginx
- Docker

### Шаблон наполнения env-файла:

DB_ENGINE=django.db.backends.postgresql # указываем, что работаем с postgresql

DB_NAME=имя базы данных

POSTGRES_USER=логин для подключения к базе данных

POSTGRES_PASSWORD=пароль для подключения к БД

DB_HOST=db # название сервиса (контейнера)

DB_PORT=5432 # порт для подключения к БД

### Как запустить проект:

Зайти на ВМ.

Выполнить миграции:
```
docker-compose exec web python manage.py migrate
```

Собрать статистику:
```
docker-compose exec web python manage.py collectstatic --no-input
```

Создать суперпользователя:
```
docker-compose exec web python manage.py createsuperuser
```

### Примеры эндпоинтов:

Регистрация нового пользователя
Получить код подтверждения на переданный email.
Права доступа: Доступно без токена.

```
http://127.0.0.1:8000/api/v1/auth/signup/
```

Получение JWT-токена
Получение JWT-токена в обмен на username и confirmation code.
Права доступа: Доступно без токена.

```
http://127.0.0.1:8000/api/v1/auth/signup/
```

Получение списка всех категорий
Получить список всех категорий
Права доступа: Доступно без токена

```
http://127.0.0.1:8000/api/v1/categories/
```

Добавление новой категории
Создать категорию.
Права доступа: Администратор.

```
http://127.0.0.1:8000/api/v1/categories/
```

Удаление категории
Удалить категорию.
Права доступа: Администратор.

```
http://127.0.0.1:8000/api/v1/categories/{slug}/
```

Подробнее можно посмотреть в документации Redoc после старта сервера по адресу:

```
http://127.0.0.1:8000/redoc/
```

### Разработчик:

Басков Михаил (baem-festa@yandex.ru)
