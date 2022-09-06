# yamdb_final
![example workflow](https://github.com/Straga33/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

Проект YaMDb собирает отзывы (Review) пользователей на произведения (Title). Произведения делятся на категории: "Книги", "Фильмы", "Музыка". Список категорий (Category) может быть расширен.
Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.

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

Создать env-файл по шаблону в директории:
```
infra_sp2/infra/
```

Собрать и запустить контейнеры, из директории infra_sp2/infra/:
```
docker-compose up -d --build 
```

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

### Разработчик:

Басков Михаил (baem-festa@yandex.ru)

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

