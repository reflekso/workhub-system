# GET /api/v1/jobs/{job_id}/proposals

Content-type: application/json 

Authorization: Bearer token

## Описание

Метод для получения списка откликов на заказ. Доступен только Заказчику, создавшему заказ.

## Path-параметры

| Название | Тип | Описание |
| --- | --- | --- |
| job_id | integer | Идентификатор заказа |

## Query-параметры

| Название | Тип | Описание |
| --- | --- | --- |
| page | integer | Номер страницы списка откликов (page > 0; default = 1) |
| per_page | integer | Количество откликов на странице (0 < per_page < 20; default = 12) |

## Response

### 200 OK
```json
{
  "data": [
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
  ],
  
  "pagination": {
    "current_page": 1,
    "per_page": 12,
    "total_items": 120,
    "total_pages": 10
  }
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
| 400 | `INVALID_PAGE` | Query-параметр `page` должен быть `integer` > 0 или отсутствовать (default=1) | `"Неверные параметры пагинации (page > 0)"` |
| 400 | `INVALID_PER_PAGE` | Query-параметр `per_page` должен быть 0 < `integer` < 20  или отсутствовать (default=12)  | `"Неверные параметры пагинации (0 < per_page < 25"` |
| 401 | `UNAUTHORIZED` | Нет токена или токен не валиден | `"Вы не авторизованы в системе."` |
| 403 | `PROPOSAL_LIST_FORBIDDEN_ROLE` | Получение списка откликов на заказ доступно только пользователям с ролью `client` | `"Только Заказчики могут смотреть список откликов."` |
| 403 | `PROPOSAL_LIST_FORBIDDEN_OWNER` | Получение списка откликов на заказ доступно только создателю заказа. | `"Вы не создатель этого заказа."` |
| 403 | `PROPOSAL_LIST_FORBIDDEN_STATUS` | Получение списка откликов на заказ недоступно для заказов в статусе `draft` | `"Заказ еще не опубликован."` |
| 404 | `JOB_NOT_FOUND` | Заказ с таким ID не найден | `"Заказ не найден."` |
| 500 | `INTERNAL_ERROR` | Внутренняя ошибка сервера | `"Внутренняя ошибка сервера."` |


## Маппинг полей

| Название поля | Тип | Описание | Соответствующий атрибут в БД |
|---|---|---|---|
| data | array | Массив откликов на заказ | - |
| proposal_id | integer | Идентификатор отклика | proposals.proposal_id |
| freelancer_id | integer | Идентификатор Исполнителя, оставившего отклик | proposals.freelancer_id |
| proposal_message | string | Сопроводительный текст Исполнителя к отклику | proposals.proposal_message |
| created_at | string | Дата и время отклика на заказ | proposals.created_at |
| pagination | array | Массив параметров пагинации | - |
| current_page | integer | Номер текущей страницы | - |
| per_page | integer | Количество элементов на странице | - |
| total_items | integer | Общее число откликов | - |
| total_pages | integer | Общее число страниц | - |
| status | integer | Код состояния HTTP | - |
| code | string | Внутренний код ошибки | - |
| title | string | Текстовый код состояния HTTP  | - |
| message | string | Поясняющее сообщение ответа | - |

