# PATCH /api/v1/jobs/{job_id}/proposals/{proposal_id}

Content-type: application/json 

Authorization: Bearer token

## Описание

Метод для выбора Исполнителя заказа, среди откликнувшихся. У выбранного Исполнителя статус отклика меняется на "accepted". Доступно только Заказчику, создавшему заказ.

## Path-параметры

| Название | Тип | Описание |
| --- | --- | --- |
| job_id | integer | Идентификатор заказа |
| proposal_id | integer | Идентификатор отклика |

## Request-Body

```
{
  "proposal_status": "accepted"
}
```

## Responses

### 200 OK

```
{
  "proposal_id": 2,
  "freelancer_id": 12,
  "freelancer_name": "Иванов Иван",
  "status": 200,
  "title": "OK",
  "message": "Исполнитель заказа успешно выбран."
  
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
  "message": "Заказ или отклик не найден."
}
```
### 409 Conflict

```
{
  "status": 409,
  "title": "Conflict",
  "message": "Исполнитель заказа уже выбран."
}
```
### 422 Unprocessable Content

```
{
  "status": 422,
  "title": "Unprocessable Content",
  "message": "Неверно переданный статус. Можно передавать только 'accepted'."
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
| proposal_status | string | Статус отклика | proposals.proposal_status |
| proposal_id | integer | Идентификатор отклика | proposals.proposal_id |
| freelancer_id | integer | Идентификатор Исполнителя, оставившего отклик | proposals.freelancer_id |
| freelancer_name | integer | Имя и фамилия Исполнителя, оставившего отклик | users.firstname, users.lastname |
| status | integer | Код состояния HTTP | - |
| title | string | Текстовый код состояния HTTP  | - |
| message | string | Поясняющее сообщение ответа | - |


