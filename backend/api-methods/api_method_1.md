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

```json
{
  "proposal_message": "Какой-то сопроводительный текст..."
}
```

## Responses

### 201 Created

```json
{
  "proposal_id": 3
}
```

## Коды ошибок

Все ошибки возвращаются в едином формате.

```json
{
  "status": 401,
  "code": "UNAUTHORIZED",
  "title": "Forbidden",
  "message": "Вы не авторизованы в системе."
}
```

| HTTP-код | `code` | Описание | `message` |
| --- | --- | --- | --- |
| 400 Bad Request | `ERROR_VALIDATION` | Ошибка валидации запроса | `"Ошибка в теле запроса."` |
| 401 Unauthorized | `UNAUTHORIZED` | Нет токена или токен не валиден | `"Вы не авторизованы в системе."` |
| 403 Forbidden | `PROPOSAL_CREATE_FORBIDDEN` | Создание отклика на заказ доступно только пользователям с ролью `freelancer` | `"Действие доступно только Исполнителям."` |
| 404 Not Found | `JOB_NOT_FOUND` | Заказ с таким ID не найден | `"Заказ не найден."` |
| 409 Conflict | `PROPOSAL_CREATE_CONFLICT_DUPLICATE` | Пользователь не может создавать отклик на один заказ дважды | `"Вы уже откликнулись на этот заказ."` |
| 409 Conflict | `PROPOSAL_CREATE_CONFLICT_STATUS` | Пользователь может создавать отклик на заказ только если он в статусе `published` | `"Сейчас нельзя откликнуться на этот заказ."` |
| 422 Unprocessable Content | `PROPOSAL_MESSAGE_TOO_LONG` | Длина сопроводительного текста не должна превышать 500 символов | `"Неверная длина сопроводительного текста. Максимально возможная длина 500 символов."` |
| 500 Internal Server Error | `INTERNAL_ERROR` | Внутренняя ошибка сервера | `"Внутренняя ошибка сервера."` |

## Маппинг полей

| Название поля | Тип | Описание | Соответствующий атрибут в БД |
|---|---|---|---|
| proposal_message | string | Сопроводительный текст к отклику | proposals.proposal_message |
| proposal_id | integer | Идентификатор отклика | proposals.proposal_id |
| status | integer | Код состояния HTTP | - |
| code | string | Внутренний код ошибки | - |
| title | string | Текстовый код состояния HTTP  | - |
| message | string | Поясняющее сообщение ответа | - |

