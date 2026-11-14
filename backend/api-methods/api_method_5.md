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

```json
{
  "proposal_status": "cancelled"
}
```

## Response

### 200 OK

```json
{
  "proposal_id": 4,
  "job_id": 7
}
```


| HTTP-код | `code` | Описание | `message` |
| --- | --- | --- | --- |
| 400 | `CLOSE_PROPOSAL_VALIDATION_ERROR` | Ошибка валидации, запрос должен содержать поле `proposal_status` | `Ошибка запроса.` |
| 401 | `UNAUTHORIZED` | Нет токена или токен не валиден | `"Вы не авторизованы в системе."` |
| 403 | `CLOSE_PROPOSAL_FORBIDDEN_ROLE` | Отмена отклика на заказ доступна только пользователям с ролью `freelancer` | `"Только Исполнители могут отменять отклик на заказ."` |
| 403 | `CLOSE_PROPOSAL_FORBIDDEN_OWNER` | Отмена отклика доступна только Исполнителю, который оставил этот отклик | `"У вас нет права отменять этот отклик."` |
| 404 | `PROPOSAL_NOT_FOUND` | Отклик с таким ID не найден | `"Отклик не найден."` |
| 409 | `CLOSE_PROPOSAL_CONFLICT` | Пользователь может отменять отклик только, если отклик в статусе `pending`  | `"Вы уже не можете отменить отклик на этот заказ."` |
| 422 | `CLOSE_PROPOSAL_UNPROCESSABLE` | В теле запроса поле `proposal_status` может содержать только `cancelled`. | `"Неверно переданный статус отклика. Статус может быть только 'cancelled'."` |
| 500 | `INTERNAL_ERROR` | Внутренняя ошибка сервера | `"Внутренняя ошибка сервера."` |


## Маппинг полей


| Название поля | Тип | Описание | Соответствующий атрибут в БД |
|---|---|---|---|
| proposal_id | integer | Идентификатор отклика | proposals.proposal_id |
| job_id | integer | Идентификатор заказа | proposals.job_id |
| proposal_status | string | Статус отклика | proposals.proposal_status |
| status | integer | Код состояния HTTP | - |
| code | string | Внутренний код ошибки | - |
| title | string | Текстовый код состояния HTTP  | - |
| message | string | Поясняющее сообщение ответа | - |
