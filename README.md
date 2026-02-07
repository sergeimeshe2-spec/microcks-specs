# Microcks API Specifications

AsyncAPI и OpenAPI спецификации для Microcks моков.

## Структура

```
microcks-specs/
├── asyncapi-kafka.yaml    # Kafka события (User Events)
├── asyncapi-http.yaml     # HTTP Webhooks (Order Webhooks)
└── README.md
```

## Использование

### Локальная синхронизация

```bash
# Авто-проверка изменений каждые 10 минут
python sync/local-sync.py --watch

# Или один раз
python sync/local-sync.py --once
```

### В Kubernetes

Спецификации монтируются в Microcks контейнер:
```yaml
volumes:
  - ./specs:/specs:ro
```

## Спецификации

### asyncapi-kafka.yaml
- **Kafka события**: UserCreated, UserUpdated, UserDeleted
- **Команды**: CreateUser, UpdateUser, DeleteUser
- **Каналы**: user-created, user-updated, user-deleted, user-commands

### asyncapi-http.yaml
- **HTTP Webhooks**: OrderCreated, OrderPaid, OrderShipped, OrderDelivered
- **Subscribe**: Endpoint `order/webhooks/{webhookId}`
- **События**: order.created, order.paid, order.shipped, order.delivered

## Обновление спецификаций

1. Измени файл в этом репозитории
2. Сделай git commit и push
3. Microcks автоматически обновит моки (через sync service)

## Связанные репозитории

- **Core**: https://github.com/sergeimeshe2-spec/microcks-custom
- **Helm**: https://github.com/sergeimeshe2-spec/microcks-helm
- **Docker**: https://github.com/sergeimeshe2-spec/microcks-docker
- **CI/CD**: https://github.com/sergeimeshe2-spec/microcks-ci
