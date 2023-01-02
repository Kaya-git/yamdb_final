# YaMDb REST API

![yamdb_tests](https://github.com/SurfimChilim/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

С проектом можете ознакомится по ссылке : hhtps://51.250.110.115:8000
## Описание

Проект реализует REST API для сервиса YaMDb — базы отзывов о различных произведениях (фильмах, книгах, музыке и др.). API предоставляет следующие возможности:
## Пользовательские роли
| Функционал                                                                                                    | Модератор |
Неавторизованные пользователи |  Авторизованные пользователи | Администратор |
|:--------------------------------------------------------------------------------------------------------------------------|:---------:|:---------:|:---------:|:---------:|
| Самостоятельная регистрация с отправкой кода подтверждения на e-mail.                                                     | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| Получение JWT токена для авторизации.                                                                                     | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| Получение информации о произведениях, отзывах к ним, просмотр комментариев.                                               | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| Получение и изменение данных своей учетной записи.                                                                        | :heavy_check_mark: | :x: | :heavy_check_mark: | :heavy_check_mark: |
| Добавление, редактирование и удаление своих отзывов на произведения.                                                      | :heavy_check_mark: | :x: | :heavy_check_mark: | :heavy_check_mark: |
| Добавление, редактирование и удаление своих комментариев к отзывам.                                                       | :heavy_check_mark: | :x: | :heavy_check_mark: | :heavy_check_mark: |
| Редактирование и удаление отзывов и комментариев других пользователей.                                                    | :heavy_check_mark: | :x: | :x: | :heavy_check_mark: |
| Добавление и удаление категорий и жанров произведений.                                                                    | :x: | :x: | :x: | :heavy_check_mark: |
| Добавление, изменение и удаление информации о произведениях.                                                              | :x: | :x: | :x: | :heavy_check_mark: |
| Регистрация новых пользователей.                                                                                          | :x: | :x: | :x: | :heavy_check_mark: |
| Просмотр и изменение информации о зарегистрированных пользователях.                                                       | :x: | :x: | :x: | :heavy_check_mark: |
| Удаление пользователей.     

## Как запустить проект:

Клонировать репозиторий и перейти в директорию проекта:

```
git clone git@github.com:hikjik/api_yamdb.git
```

```
cd api_yamdb
```

Создать и активировать виртуальное окружение:

```
python3 -m venv env
```

```
source env/bin/activate
```

Установить зависимости из файла requirements.txt:

```
python3 -m pip install --upgrade pip
```

```
pip install -r requirements.txt
```

Выполнить миграции:

```
python3 manage.py migrate
```

Запустить проект:

```
python3 manage.py runserver
```

Загрузка тестовых данных:

```
python3 manage.py load_data
```

## Документация

После запуска проекта документация доступна по [ссылке.](http://127.0.0.1:8000/redoc)

## Примеры запросов к API

1. Самостоятельная регистрация с отправкой кода подтверждения на e-mail

```
POST /api/v1/auth/signup/
```

Тело запроса:

```json
{
    "username": "martin",
    "email": "martin@mail.ru"
}
```

Пример ответа:

```json
{
    "username": "martin",
    "email": "martin@mail.ru"
}
```

2. Получение JWT токена

```
POST /api/v1/auth/signup/
```

Тело запроса:

```json
{
    "username": "martin",
    "confirmation_code": "62v-e034fd8e1432fb4c2701"
}
```

Пример ответа:

```json
{
    "token": "string"
}
```

3. Получение списка произведений

```
GET /api/v1/titles?year=1971&category=music&genre=rock&name=deep
```

Пример ответа:

```json
{
    "count": 1,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": 30,
            "name": "Deep Purple — Smoke on the Water",
            "year": 1971,
            "rating": 10,
            "description": "",
            "genre": [
                {
                    "name": "Рок",
                    "slug": "rock"
                }
            ],
            "category": {
                "name": "Музыка",
                "slug": "music"
            }
        }
    ]
}
```
## Шаблон наполнения env файла
- указываем, что работаем с postgresql
```
DB_ENGINE=django.db.backends.postgresql 
```
- имя базы данных
```
DB_NAME=postgres 
```
- логин для подключения к базе данных
```
POSTGRES_USER=postgres 
```
- пароль для подключения к БД (установите свой)
```
POSTGRES_PASSWORD=postgres
```
- название сервиса (контейнера)
```
DB_HOST=db
```
- порт для подключения к БД
```
DB_PORT=5432
```
## Описание команд для запуска приложения в контейнерах
- Запускаем контейнер в терминале командой:
```
docker run --name <имя контейнера> -it -p 8000:8000 yamdb
```
- Останавливаем контейнер командой:
```
docker container start <CONTAINER ID>
```
## Описание команд для заполнения бд:
```
docker-compose exec web python manage.py migrate
```
docker-compose exec web python manage.py createsuperuser
```
docker-compose exec web python manage.py collectstatic --no-input
```
## Использованные технологии:
- Python 3.7
- Django Framework 2.2.16
- Django Rest Framework 3.12.4
- Docker 20.10.17
- Docker Compose v2.10.2
- Nginx 1.23.2
- Gunicorn 20.0.4
- PostgreSql v15
## Об авторе:
- Начинающий разработчик Евгений Бузуев. С моими другими работами вы можете ознакомится по ссылке: https://github.com/SurfimChilim
