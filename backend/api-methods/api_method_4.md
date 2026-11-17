# GET /api/v1/users/me/proposals

Content-type: application/json 

Authorization: Bearer token

## Описание

Метод для получения оставленных Исполнителем откликов. Доступно только Исполнителям.

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
      "proposal_id": 2,
      "job_id": 4,
      "job_name": "Разработка веб-сайта",
      "created_at": "2026-01-01T05:40:04Z",
      "proposal_status": "pending"
    },
    {
      "proposal_id": 6,
      "job_id": 2,
      "job_name": "Создание дизайна",
      "created_at": "2026-01-05T06:20:04Z",
      "proposal_status": "cancelled"
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
| 403 | `GET_MY_PROPOSALS_FORBIDDEN_ROLE` | Просмотр списка своих откликов на заказы доступен только пользователям с ролью `freelancer` | `"Только Исполнители могут просматривать список своих откликов."` |
| 500 | `INTERNAL_ERROR` | Внутренняя ошибка сервера | `"Внутренняя ошибка сервера."` |


## Маппинг полей

| Название поля | Тип | Описание | Соответствующий атрибут в БД |
|---|---|---|---|
| data | array | Массив откликов Исполнителя | - |
| proposal_id | integer | Идентификатор отклика | proposals.proposal_id |
| job_id | integer | Идентификатор заказа | proposals.job_id |
| job_name | string | Название заказа | jobs.job_name |
| created_at | string | Дата и время отклика на заказ | proposals.created_at |
| proposal_status | string | Статус отклика | proposals.proposal_status |
| pagination | array | Массив параметров пагинации | - |
| current_page | integer | Номер текущей страницы | - |
| per_page | integer | Количество элементов на странице | - |
| total_items | integer | Общее число откликов Исполнителя | - |
| total_pages | integer | Общее число страниц | - |
| status | integer | Код состояния HTTP | - |
| code | string | Внутренний код ошибки | - |
| title | string | Текстовый код состояния HTTP  | - |
| message | string | Поясняющее сообщение ответа | - |


