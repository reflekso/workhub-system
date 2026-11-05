# PATCH /api/v1/users/me/proposals/{proposal_id}

Content-type: application/json 

Authorization: Bearer token

## Описание

Метод для отмены отклика на заказ. Доступно только Исполнителю, оставившему отклик на заказ.

## Path-параметры


| Название | Тип | Описание |
| --- | --- | --- |
| proposal_id | integer | Идентификатор отклика |

## Request-Body

```
{
  "proposal_status": "cancelled"
}
```

## Responses

### 200 OK

```
{
  "proposal_id": 4,
  "job_id": 7
}
```

### 400 Bad Request

```
{
  "status": 400,
  "title": "Bad Request",
  "message": "Ошибка запроса."
}
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
  "message": "Отклик не найден."
}
```
### 409 Conflict

```
{
  "status": 409,
  "title": "Conflict",
  "message": "Исполнитель уже закрыл заказ или заказ передан в работу."
}
```
### 422 Unprocessable Content

```
{
  "status": 422,
  "title": "Unprocessable Content",
  "message": "Неверно переданный статус. Можно передавать только 'cancelled'."
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
| proposal_status | string | Статус отклика | proposals.proposal_status |
| status | integer | Код состояния HTTP | - |
| title | string | Текстовый код состояния HTTP  | - |
| message | string | Поясняющее сообщение ответа | - |
