# Satis Composer Registry (Docker, без авторизации)

Приватный Composer-регистр на базе **Satis** + **Nginx**.

## Структура

```
satis-registry/
├── satis.json           ← список репозиториев и пакетов
├── docker-compose.yml
└── nginx/
    └── default.conf     ← раздача без авторизации
```

## Запуск

```bash
# 1. Сборка пакетов (запускается разово)
docker compose run --rm satis

# 2. Поднять nginx
docker compose up -d nginx
```

Регистр доступен на `http://localhost:*.env.PORT*`.

Пересборка при добавлении пакетов:

```bash
docker compose run --rm satis
```

## Использование в проектах composer.json

```json
{
  "name": "mycompany/myproject",
  "config": {
    "secure-http": false // если нет https
  },
  "require": {
    "monolog/monolog": "3.0",
    "phpstan/phpstan": "2.0"
  },
  "repositories": [
    {
      "type": "composer",
      "url": "http://localhost:8089" // *
    },
    {
      "packagist.org": false // чтобы не тянуть зависимости из packagist.org
    }
  ]
}
```
####  * url необходимо указать такой же как и в параметре "homepage" в satis.json
```json
"homepage": "http://localhost:*.env.PORT*",
```
