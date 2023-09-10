## Описание проекта

Сайт для планирования дел.

## Возможности
- Создание задач и планов а также их выполнение.

## Технологии
- React
- Django
- DRF

## Infra
- Nginx
- Gunicorn
- Docker
- Docker-compose

## CI/CD
- Github Actions

## Запуск проекта из образов с Docker hub

Для запуска необходимо на создать папку проекта, например `taski` и перейти в нее:

```shell notranslate position-relative overflow-auto
mkdir taski
cd taski
```

В папку проекта скачиваем файл `docker-compose.production.yml` и запускаем его:

```shell notranslate position-relative overflow-auto
sudo docker compose -f docker-compose.production.yml up
```

Произойдет скачивание образов, создание и включение контейнеров, создание томов и сети.

## Запуск проекта из исходников GitHub

Клонируем себе репозиторий:

```shell notranslate position-relative overflow-auto
git clone git@github.com:Gennady-Umikashvili/taski-docker.git
```

Выполняем запуск:

```shell notranslate position-relative overflow-auto
sudo docker compose -f docker-compose.yml up
```

## После запуска: Миграции, сбор статистики

После запуска необходимо выполнить сбор статистики и миграции бэкенда. Статистика фронтенда собирается во время запуска контейнера, после чего он останавливается.

```shell notranslate position-relative overflow-auto
sudo docker compose -f [имя-файла-docker-compose.yml] exec backend python manage.py migrate

sudo docker compose -f [имя-файла-docker-compose.yml] exec backend python manage.py collectstatic

sudo docker compose -f [имя-файла-docker-compose.yml] exec backend cp -r /app/collected_static/. /static/static/
```

И далее проект доступен на:

```
http://localhost:8000/
```

## Необходимые переменные окружения

```shell notranslate position-relative overflow-auto
POSTGRES_USER= <Желаемое_имя_пользователя_базы_данных>
POSTGRES_PASSWORD= <Желаемый_пароль_пользователя_базы_данных>
POSTGRES_DB= <Желаемое_имя_базы_данных>
DB_HOST=
DB_PORT= 
SECRET_KEY = 
DEBUG = 
```

## Остановка оркестра контейнеров

В окне, где был запуск **Ctrl+С** или в другом окне:

```shell notranslate position-relative overflow-auto
sudo docker compose -f docker-compose.yml down
```
### Автор
Геннадий Умикашвили: [github](https://github.com/Gennady-Umikashvili)
