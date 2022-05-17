# CI и CD проекта api_yamdb
>Учебный проект в рамках курса __Backend-developer__ на платформе __Яндекс.Практикум__

### Стек технологий:

[![Python](https://camo.githubusercontent.com/f13f8c8fd603bd94f3c006d5650ea82b0213e94c54ac4b93e1d56f765a068882/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4d616465253230776974682d507974686f6e2d677265656e3f6c6f676f3d707974686f6e266c6f676f436f6c6f723d776869746526636f6c6f72)](https://www.python.org/) [![Docker](https://camo.githubusercontent.com/68b1b15acde4efc8a882ad9dc399d73a7d72d6ffb69fd47f95c60772976d1218/68747470733a2f2f696d672e736869656c64732e696f2f7374617469632f76313f6d6573736167653d646f636b6572266c6f676f3d646f636b6572266c6162656c436f6c6f723d35633563356326636f6c6f723d303032633636266c6f676f436f6c6f723d7768697465266c6162656c3d253230267374796c653d706c6173746963)](https://www.docker.com/) [![Django](https://camo.githubusercontent.com/36cd67e6d0292012b0c84f7ca1c60697fe15d9c2a5a8171d2229a877f321298d/68747470733a2f2f696d672e736869656c64732e696f2f7374617469632f76313f6d6573736167653d646a616e676f266c6f676f3d646a616e676f266c6162656c436f6c6f723d35633563356326636f6c6f723d306334623333266c6f676f436f6c6f723d7768697465266c6162656c3d253230267374796c653d706c6173746963)](https://www.djangoproject.com/) [![Nginx](https://camo.githubusercontent.com/ea3d94458fad94b44b35ed0d03b6cf7bc2054d334d6f669f29807fa7a52ab90d/68747470733a2f2f696d672e736869656c64732e696f2f7374617469632f76313f6d6573736167653d6e67696e78266c6f676f3d6e67696e78266c6162656c436f6c6f723d35633563356326636f6c6f723d303039393030266c6f676f436f6c6f723d7768697465266c6162656c3d253230267374796c653d706c6173746963)](https://nginx.org/) [![Postgres](https://camo.githubusercontent.com/ad8e4b6c04b8f9caec8d7c47e9d79110724148c57282007ca247424871f3626f/68747470733a2f2f696d672e736869656c64732e696f2f7374617469632f76313f6d6573736167653d706f737467726573716c266c6f676f3d706f737467726573716c266c6162656c436f6c6f723d35633563356326636f6c6f723d313138326333266c6f676f436f6c6f723d7768697465266c6162656c3d253230267374796c653d706c6173746963)](https://www.postgresql.org/) ![workflow](https://github.com//MaksimZAHM/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

### Описание
В проекте YaMDb реализован API с помощью Django REST Framework, его задача собирать отзывы (Review) пользователей на произведения (Titles). Произведения делятся на категории: «Книги», «Фильмы», «Музыка».
Пользователи оставляют к произведениям текстовые отзывы (Review) и ставят произведению оценку в диапозоне от одного до десяти (целое число).
Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.

### Ресурсы API  __YaMDb__ :

* Ресурс auth: аутентификация.
* Ресурс users: пользователи.
* Ресурс titles: произведения, к которым пишут отзывы (определённый фильм, книга или песенка).
* Ресурс categories: категории (типы) произведений («Фильмы», «Книги», «Музыка»).
* Ресурс genres: жанры произведений. Одно произведение может быть привязано к нескольким жанрам.
* Ресурс reviews: отзывы на произведения. Отзыв привязан к определённому произведению.
* Ресурс comments: комментарии к отзывам. Комментарий привязан к определённому отзыву.

__Ознакомиться с полным функционалом и примерами можно по адресу__   
__http://[адрес вашего сервера/ip]/redoc__  
__( Доступно после запуска проекта )__

### Запуск проекта 
Убедитесь, что у вас установлен Docker командой:

```
docker -v
```

Клонировать репозиторий и перейти в него в командной строке. Создать и активировать виртуальное окружение c учетом версии Python 3.7:

```
git clone https://github.com/MaksimZAHM/yamdb_final.git
```

Cоздать и активировать виртуальное окружение:

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

Перейдите в папку с файлом docker-compose.yaml:

```
cd infra
```

Разверните контейнеры:

```
docker-compose up -d --build
```

Выполните миграции, создайте суперпользователя, соберите статику:

```
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
docker-compose exec web python manage.py collectstatic --no-input
```


Создайте дамп (резервную копию) базы:

```
docker-compose exec web python manage.py dumpdata > fixtures.json
```

Остановить приложение в контейнерах:


```
docker-compose down -v
```

Запуск pytest (при запущенном виртуальном окружении):


```
cd yamdb_final && pytest
```

### Документация API с примерами: /redoc/
шаблон наполнения env-файла
см.
infra/.env.template
описание команды для заполнения базы данными
`cd api_yamdb && python manage.py loaddata ../infra/fixtures.json`

### Приложение работает по ссылкам:
http://51.250.104.25/admin/
http://51.250.104.25/redoc/

### Разработчик проекта

Автор: Maksim Zamyatin  
E-mail: [mm.zamyatin@gmail.com](mailto:mm.zamyatin@gmail.com)
