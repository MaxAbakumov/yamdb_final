# infra_sp2
## ***Проект YaMDb в контейнере***

Данный проект предназначен для развертывания проекта YaMDb из контейнеров Docker.

В проекте имеется файл .env. Он существует для того, чтобы там прописывать переменные окружения.
#### Пример:

```
DB_ENGINE=django.db.backends.postgresql # указываем, что работаем с postgresql
DB_NAME=postgres # имя базы данных
POSTGRES_USER=postgres # логин для подключения к базе данных
POSTGRES_PASSWORD=postgres # пароль для подключения к БД (установите свой)
DB_HOST=db # название сервиса (контейнера)
DB_PORT=5432 # порт для подключения к БД 
```

#### Как запустить проект
Для запуска контейнера перейдите в директорию с файлом ***docker-compose*** и выполните команду:

```
docker-compose up
```

Теперь в контейнере web нужно выполнить миграции, создать суперпользователя и собрать статику. Команды внутри контейнеров выполняют посредством подкоманды docker-compose exec. Это эквивалент docker exec: с её помощью можно выполнять произвольные команды в сервисах внутри контейнеров.
Выполните по очереди команды:

```
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
docker-compose exec web python manage.py collectstatic --no-input 
```

Теперь проект доступен по адресу http://localhost/.

Примеры обращений к эндпоинтам находятся по адресу http://localhost/redoc/

Для заполнения базы данными, используйте команду:

```
docker-compose exec web python manage.py loaddata fixtures.json
```

Бейдж отображения состояния:

```
https://github.com/MaxAbakumov/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg
```
Ссылка на проект:

```
http://51.250.107.2/admin/
```

Автор: Абакумов Максим