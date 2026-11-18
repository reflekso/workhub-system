[Главная](/README.md) / [Техническое задание](/requirements-specification.md) / [Backend: API-методы](/backend/api.md) / [PATCH /api/v1/jobs/{job_id}/proposals/{proposal_id}](/backend/api-methods/api_method_3.md)

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

```json
{
  "proposal_status": "accepted"
}
```

## Response

### 200 OK

```json
{
  "proposal_id": 2,
  "freelancer_id": 12,
  "freelancer_name": "Иванов Иван" 
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
| 400 | `CHOOSE_FREELANCER_VALIDATION_ERROR` | Ошибка валидации, запрос должен содержать поле `proposal_status` | `Ошибка запроса.` |
| 401 | `UNAUTHORIZED` | Нет токена или токен не валиден | `"Вы не авторизованы в системе."` |
| 403 | `CHOOSE_FREELANCER_FORBIDDEN_ROLE` | Выбор Исполнителя заказа доступен только пользователям с ролью `client` | `"Только Заказчики могут выбирать Исполнеителя."` |
| 403 | `CHOOSE_FREELANCER_FORBIDDEN_OWNER` | Выбор Исполнителя заказа доступен только создателю заказа. | `"Вы не создатель этого заказа."` |
| 404 | `JOB_NOT_FOUND` | Заказ с таким ID не найден | `"Заказ не найден."` |
| 404 | `PROPOSAL_NOT_FOUND` | Отклик с таким ID не найден | `"Отклик не найден."` |
| 409 | `CHOOSE_FREELANCER_CONFLICT_JOB` | Пользователь может выбирать Исполнителя заказа только, если заказ в статусе `published`  | `"Вы не можете выбрать Исполнителя на этот заказ."` |
| 409 | `CHOOSE_FREELANCER_CONFLICT_PROPOSAL` | Пользователь может выбрать Исполнителя только если его отклик в статусе `pending`  | `"Вы не можете выбрать этого Исполнителя."` |
| 422 | `CHOOSE_FREELANCER_UNPROCESSABLE` | В теле запроса поле `proposal_status` может содержать только `accepted`. | `"Неверно переданный статус отклика. Статус может быть только 'accepted'."` |
| 500 | `INTERNAL_ERROR` | Внутренняя ошибка сервера | `"Внутренняя ошибка сервера."` |

## Маппинг полей

| Название поля | Тип | Описание | Соответствующий атрибут в БД |
|---|---|---|---|
| proposal_status | string | Статус отклика | proposals.proposal_status |
| proposal_id | integer | Идентификатор отклика | proposals.proposal_id |
| freelancer_id | integer | Идентификатор Исполнителя, оставившего отклик | proposals.freelancer_id |
| freelancer_name | integer | Имя и фамилия Исполнителя, оставившего отклик | users.firstname, users.lastname |
| status | integer | Код состояния HTTP | - |
| code | string | Внутренний код ошибки | - |
| title | string | Текстовый код состояния HTTP  | - |
| message | string | Поясняющее сообщение ответа | - |


