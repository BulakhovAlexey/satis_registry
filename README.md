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

## Использование в composer.json

```json
{
  "repositories": [
    { "type": "composer", "url": "http://localhost:*.env.PORT*" }
  ],
  "require": {
    "example/my-private-package": "^1.0"
  }
}
```
### url необходимо указать такой же как и в параметре "homepage" в satis.json
```json
"homepage": "http://localhost:*.env.PORT*",
```
