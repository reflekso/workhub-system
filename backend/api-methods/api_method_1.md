# POST /api/v1/jobs/{job_id}/proposals

Content-type: application/json 

Authorization: Bearer token

## Описание

Метод для оставления отклика на заказ. Доступен только Исполнителям.

## Path-параметры

| Название | Тип | Описание |
| --- | --- | --- |
| job_id | integer | Идентификатор заказа |

## Request-Body

```
{
  "freelancer_id": 2,
  "proposal_message": "Какой-то сопроводительный текст..."
}
```

## Responses

### 201 Created

```
{
  "proposal_id": 3
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
  "message": "Заказ не найден."
}
```
### 409 Conflict

```
{
  "status": 409,
  "title": "Conflict",
  "message": "Вы уже откликнулись на этот заказ."
}
```
### 422 Unprocessable Content

```
{
  "status": 422,
  "title": "Unprocessable Content",
  "message": "Неверная длина сопроводительного текста. Максимально возможная длина 500 символов."
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
| freelancer_id | integer | Идентификатор пользователя, вызывающего метод | proposals.freelancer_id |
| proposal_message | string | Сопроводительный текст к отклику | proposals.proposal_message |
| proposal_id | integer | Идентификатор отклика | proposals.proposal_id |
| status | integer | Код состояния HTTP | - |
| title | string | Текстовый код состояния HTTP  | - |
| message | string | Поясняющее сообщение ответа | - |

