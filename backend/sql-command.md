# SQL-запросы, используемые при обращении к БД

## Описание

SQL-запросы распределены по функциональным требованиям к Backend. Запросы нельзя полностью копировать и использовать, в некоторых из них описаны бизнес-требования.

## BE-1

### Проверка существования заказа и его статуса

```sql
SELECT job_status
FROM jobs 
WHERE job_id = 'ID заказа в запросе'
```

**Responses:** 

1. `job_status`, если заказ создан.
2. Пустой ответ, если заказ не создан.

---

### Проверка отклика Исполнителя на заказ

```sql
SELECT 1
FROM proposals
WHERE job_id = 'ID заказа в запросе' AND freelancer_id = 'ID Исполнителя, отправившего запрос'
```

**Responses:**

1. `1`, если Исполнитель уже откликался на заказ.
2. Пустой ответ, если Исполнитель не откликался на заказ.

---

### Создание отклика на заказ

```sql
INSERT INTO proposals(job_id, freelancer_id, proposal_message) 
VALUES (ID заказа, ID Исполнителя, 'Сопроводительный текст')
```

**Responses:**

1. Успешное создание отклика, возврат `proposal_id` нового отклика.

---

## BE-2

### Проверка существования заказа, его статуса и владельца

```sql
SELECT client_id, job_status 
FROM jobs
WHERE job_id = 'ID заказа в запросе'
```

**Responses:**

1. Пустой ответ, если заказ не создан.
2. `job_status` и `client_id`, если заказ создан.

---

### Получение списка откликов на заказ

```sql
SELECT proposals.proposal_id, proposals.freelancer_id, users.firstname, users.lastname, proposals.proposal_message, proposals.proposal_status, proposals.created_at
FROM proposals
INNER JOIN users ON users.user_id = proposals.freelancer_id
WHERE job_id = 'ID заказа в запросе'
LIMIT (per_page; default = 12)
OFFSET ((page - 1) * per_page; default = 1)
```

**Responses:**

1. Записи откликов на заказ, если они есть.
2. Пустой ответ, если откликов нет.

---

### Получение общего числа откликов на заказ

```sql
SELECT COUNT(*)
FROM proposals
WHERE job_id = 'ID заказа в запросе'
```

**Responses:**

1. Общее число откликов на заказ, если они есть.
2. `0`, если откликов нет. 

---

## BE-3

### Проверка существования заказа, его статуса и владельца

```sql
SELECT client_id, job_status 
FROM jobs
WHERE job_id = 'ID заказа в запросе'
```

**Responses:**

1. Пустой ответ, если заказ не создан.
2. `job_status` и `client_id`, если заказ создан.

---

### Проверка существования отклика и получение ID Исполнителя

```sql
SELECT freelancer_id, proposal_status
FROM proposals
WHERE proposal_id = 'ID отклика в запросе'
```

**Responses:**

1. Пустой ответ, если отклик не создан.
2. `freelancer_id` и `proposal_status`, если отклик создан.

---

### Выбор Исполнителя заказа через транзакцию

```sql
BEGIN;

UPDATE proposals
SET proposal_status = CASE
  WHEN proposal_id = 'ID отклика в запросе' THEN proposal_status = 'accepted'
  ELSE proposal_status = 'rejected'
END
WHERE job_id = 'ID заказа в запросе';

UPDATE jobs
SET freelancer_id = 'ID исполнителя из SQL-запроса выше'
WHERE job_id = 'ID заказа в запросе';

COMMIT;

```
**Responses:**

1. Транзакция успешно выполнена.

---

## BE-4

### Получение списка откликов Исполнителя 

```sql
SELECT proposals.proposal_id, proposals.job_id, jobs.job_name, proposals.created_at, proposals.proposal_status
FROM proposals
INNER JOIN jobs ON jobs.job_id = proposals.job_id 
WHERE proposals.freelancer_id = 'ID Исполнителя, отправившего запрос'
LIMIT (per_page; default = 12)
OFFSET ((page - 1) * per_page; default = 1)) 
```
**Responses:**

1. Записи откликов Исполнителя, если они есть.
2. Пустой ответ, если откликов нет.

---

### Получение общего числа откликов на заказ

```sql
SELECT COUNT(*)
FROM proposals
WHERE freelancer_id = 'ID Исполнителя, отправившего запрос'
```

**Responses:**

1. Общее число откликов Исполнителя, если они есть.
2. `0`, если откликов нет. 

---

## BE-5


### Проверка существования отклика и получение ID создателя отклика 

```sql
SELECT freelancer_id, proposal_status
FROM proposals
WHERE proposal_id = 'ID отклика в запросе'
```

**Responses:**

1. Пустой ответ, если отклик не создан.
2. `freelancer_id` и `proposal_status`, если отклик создан.

### Отмена отклика

```sql
UPDATE proposals
SET proposal_status = 'cancelled'
WHERE proposal_id = 'ID отклика в запросе'
```

**Responses:**

1. Успешное изменение статуса отклика.


