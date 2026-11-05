# GET /api/v1/users/me/proposals

Content-type: application/json 

Authorization: Bearer token

## Описание

Метод для получения оставленных Исполнителем откликов. Доступно только Исполнителям.

## Responses

### 200 OK 

```
[
  {
    "proposal_id": 2,
    "job_id": 4,
    "created_at": "2026-01-01T05:40:04Z",
    "proposal_status": "pending"
  },
  {
    "proposal_id": 6,
    "job_id": 2,
    "created_at": "2026-01-05T06:20:04Z",
    "proposal_status": "cancelled"
  }
]
```

### 401 Unauthorized


```
{
  "status": 401,
  "title": "Unauthorized",
  "message": "Вы не авторизованы в системе."
}
```

### 403 Forbidden

```
{
  "status": 403,
  "title": "Forbidden",
  "message": "У вас недостаточно прав для выполнения данного действия."
}
```
### 404 Not Found

```
{
  "status": 404,
  "title": "Not Found",
  "message": "Заказ не найден."
}
```

### 500 Internal Server Error

```
{
  "status": 500,
  "title": "Internal Server Error",
  "message": "Внутренняя ошибка сервера."
}
```
### 503 Service Unavailable

```
{
  "status": 503,
  "title": "Service Unavailable",
  "message": "Сервис временно недоступен."
}
```

## Маппинг полей

| Название поля | Тип | Описание | Соответствующий атрибут в БД |
|---|---|---|---|
| proposal_id | integer | Идентификатор отклика | proposals.proposal_id |
| job_id | integer | Идентификатор заказа | proposals.job_id |
| created_at | string | Дата и время отклика на заказ | proposals.created_at |
| proposal_status | string | Статус отклика | proposals.proposal_status |
| status | integer | Код состояния HTTP | - |
| title | string | Текстовый код состояния HTTP  | - |
| message | string | Поясняющее сообщение ответа | - |


