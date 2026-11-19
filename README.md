# WorkHub — Задание на доработку системы управления заказами для фрилансеров

![Status](https://img.shields.io/badge/Status-Documentation_Ready-brightgreen?style=flat-square)
![Role](https://img.shields.io/badge/Role-System_Analyst-blue?style=flat-square)
![API](https://img.shields.io/badge/API-REST_JSON-orange?style=flat-square)
![Database](https://img.shields.io/badge/Database-PostgreSQL-336791?style=flat-square)
![Diagrams](https://img.shields.io/badge/Diagrams-UML_Sequence_&_ERD-purple?style=flat-square)
![Docs](https://img.shields.io/badge/Docs-Markdown-lightgrey?style=flat-square)

В репозитории представлена системно-аналитическая и проектная документация, подготовленная в рамках **задания на доработку системы WorkHub** — веб-платформы для публикации заказов, сбора откликов фрилансеров и сопровождения сделок между заказчиками и исполнителями.

В ходе проектирования были формализованы бизнес-контекст задачи и техническое задание (ТЗ), обновлена модель данных и SQL-скрипты, описана серверная бизнес-логика, задокументированы контракты методов REST API со схемами взаимодействия (Sequence-диаграммами), а также подготовлены требования к интеграции и доработке клиентской части.

---

## Навигация по документации

### 1. Бизнес-контекст и техническое задание
* **[Бизнес-контекст и постановка задачи (`business-task.md`)](./business-task.md)** — описание текущей системы, цели доработки, пользовательские сценарии (User Stories).
* **[Техническое задание (`requirements-specification.md`)](./requirements-specification.md)** — общие требования к доработке системы.

### 2. Проектирование бэкенда и базы данных (`backend/`)
* **[Модель базы данных (`database.md`)](./backend/database.md)** — описание сущностей, атрибутов, связей и изменений в структуре хранения данных (визуальная схема представлена на **[ER-диаграмме](./diagrams/erd.png)**).
* **[SQL-скрипты (`sql-command.md`)](./backend/sql-command.md)** — DDL/DML-запросы для создания, модификации таблиц и выборки данных.
* **[Серверная логика (`server-logic.md`)](./backend/server-logic.md)** — бизнес-правила обработки запросов, валидация параметров, проверка прав доступа и сценарии работы бэкенда.
* **[REST API (`api.md`)](./backend/api.md)** — обзорная точка входа в спецификацию эндпоинтов:
  * [Метод API №1 (`api_method_1.md`)](./backend/api-methods/api_method_1.md) — [Sequence-диаграмма BE-1](./diagrams/sequence/be1-sequence.png)
  * [Метод API №2 (`api_method_2.md`)](./backend/api-methods/api_method_2.md) — [Sequence-диаграмма BE-2](./diagrams/sequence/be2-sequence.png)
  * [Метод API №3 (`api_method_3.md`)](./backend/api-methods/api_method_3.md) — [Sequence-диаграмма BE-3](./diagrams/sequence/be3-sequence.png)
  * [Метод API №4 (`api_method_4.md`)](./backend/api-methods/api_method_4.md) — [Sequence-диаграмма BE-4](./diagrams/sequence/be4-sequence.png)
  * [Метод API №5 (`api_method_5.md`)](./backend/api-methods/api_method_5.md) — [Sequence-диаграмма BE-5](./diagrams/sequence/be5-sequence.png)

### 3. Проектирование фронтенда (`frontend/`)
* **[Интеграция с API (`api-integration.md`)](./frontend/api-integration.md)** — порядок вызова эндпоинтов со стороны клиента, обработка состояний и передача данных.
* **[Разработка интерфейса (`ui-development.md`)](./frontend/ui-development.md)** — требования к пользовательскому интерфейсу и отображению элементов экранов.

### 4. Диаграммы (`diagrams/`)
* **[ER-диаграмма (`erd.png`)](./diagrams/erd.png)** — схема связей сущностей базы данных.
* **Sequence-диаграммы (`sequence/`)** — диаграммы последовательности для каждого метода бэкенда: [`be1-sequence.png`](./diagrams/sequence/be1-sequence.png), [`be2-sequence.png`](./diagrams/sequence/be2-sequence.png), [`be3-sequence.png`](./diagrams/sequence/be3-sequence.png), [`be4-sequence.png`](./diagrams/sequence/be4-sequence.png), [`be5-sequence.png`](./diagrams/sequence/be5-sequence.png).

---

## Структура репозитория

```text
workhub-system/
├── README.md                          # Описание проекта и навигация по документации
├── business-task.md                   # Бизнес-контекст и описание задачи на доработку
├── requirements-specification.md      # Техническое задание
├── backend/
│   ├── api.md                         # Обзор методов REST API
│   ├── database.md                    # Проектирование модели базы данных
│   ├── server-logic.md                # Описание серверной бизнес-логики (функциональные и нефункциональные требования)
│   ├── sql-command.md                 # SQL-команды и запросы к БД
│   └── api-methods/                   # Спецификации отдельных методов REST API
│       ├── api_method_1.md
│       ├── api_method_2.md
│       ├── api_method_3.md
│       ├── api_method_4.md
│       └── api_method_5.md
├── frontend/
│   ├── api-integration.md             # Сценарии интеграции клиентской части с REST API (функциональные и нефункциональные требования)
│   └── ui-development.md              # Требования к разработке пользовательского интерфейса
└── diagrams/
    ├── erd.png                        # ER-диаграмма базы данных
    └── sequence/                      # Диаграммы последовательности взаимодействия компонентов
        ├── be1-sequence.png
        ├── be2-sequence.png
        ├── be3-sequence.png
        ├── be4-sequence.png
        └── be5-sequence.png
