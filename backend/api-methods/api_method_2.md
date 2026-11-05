# GET /api/v1/jobs/{job_id}/proposals

Content-type: application/json 

Authorization: Bearer token

## Описание

Метод для получения списка откликов на заказ. Доступен только Заказчику, создавшему заказ.

## Path-параметры

| Название | Тип | Описание |
| --- | --- | --- |
| job_id | integer | Идентификатор заказа |

## Responses

### 200 OK
```
[
  {
    "proposal_id": 1,
    "freelancer_id": 20,
    "proposal_message": "Какой-то сопроводительный текст...",
    "created_at": "2026-01-01T05:40:04Z"
  },

  {
    "proposal_id": 2,
    "freelancer_id": 32,
    "proposal_message": "Другой какой-то сопроводительный текст",
    "created_at": "2026-01-01T05:40:04Z"
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
| freelancer_id | integer | Идентификатор Исполнителя, оставившего отклик | proposals.freelancer_id |
| proposal_message | string | Сопроводительный текст Исполнителя к отклику | proposals.proposal_message |
| created_at | string | Дата и время отклика на заказ | proposals.created_at |
| status | integer | Код состояния HTTP | - |
| title | string | Текстовый код состояния HTTP  | - |
| message | string | Поясняющее сообщение ответа | - |

