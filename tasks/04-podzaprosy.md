# Подзапросы

[← Ко всем темам](../README.md)

## 57. Самые дорогие товары каталога

*лёгкая* · Диалекты: PostgreSQL, ClickHouse

Дизайнер главной страницы хочет показать карточку «премиум-товар» — товар с самой высокой ценой в каталоге. Если несколько товаров стоят одинаково дорого и делят первое место, покажите их всех. Верните `id`, название и цену товара. Отсортируйте результат по `id`.

**Таблицы:**

- **customers**: `id` serial 🔑 — Идентификатор клиента; `name` varchar(100) — Имя клиента; `country` varchar(2) — Страна клиента; `registered_at` date — Дата регистрации
- **products**: `id` serial 🔑 — Идентификатор товара; `name` varchar(100) — Название товара; `category` varchar(50) — Категория товара; `price` numeric(10, 2) — Цена товара
- **orders**: `id` serial 🔑 — Идентификатор заказа; `customer_id` int → customers.id — Идентификатор клиента; `status` varchar(20) — Статус заказа; `total` numeric(10, 2) — Сумма заказа; `created_at` date — Дата создания заказа
- **order_items**: `order_id` int 🔑 — Идентификатор заказа; `product_id` int 🔑 — Идентификатор товара; `quantity` int — Количество товара

**Колонки ответа:** `id`, `name`, `price`

**Пример ответа (первые строки):**

| id | name | price |
|---|---|---|
| 9 | Шкаф | 12000.00 |
| 10 | Диван | 12000.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/easy-subq-most-expensive-product?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 58. Заказы российских клиентов

*лёгкая* · Диалекты: PostgreSQL, ClickHouse

Бухгалтер закрывает квартал и готовит выгрузку заказов только по российским клиентам — это нужно для отчёта по РФ-юрлицу. Найдите заказы клиентов, у которых страна равна `RU`. Верните `id` заказа, `customer_id` и сумму заказа. Отсортируйте результат по `id` заказа.

**Таблицы:**

- **customers**: `id` serial 🔑 — Идентификатор клиента; `name` varchar(100) — Имя клиента; `country` varchar(2) — Страна клиента; `registered_at` date — Дата регистрации
- **products**: `id` serial 🔑 — Идентификатор товара; `name` varchar(100) — Название товара; `category` varchar(50) — Категория товара; `price` numeric(10, 2) — Цена товара
- **orders**: `id` serial 🔑 — Идентификатор заказа; `customer_id` int → customers.id — Идентификатор клиента; `status` varchar(20) — Статус заказа; `total` numeric(10, 2) — Сумма заказа; `created_at` date — Дата создания заказа
- **order_items**: `order_id` int 🔑 — Идентификатор заказа; `product_id` int 🔑 — Идентификатор товара; `quantity` int — Количество товара

**Колонки ответа:** `id`, `customer_id`, `total`

**Пример ответа (первые строки):**

| id | customer_id | total |
|---|---|---|
| 1 | 1 | 350.00 |
| 2 | 1 | 2500.00 |
| 3 | 1 | 1200.00 |
| 5 | 3 | 450.00 |
| 6 | 3 | 990.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/easy-subq-orders-from-ru-customers?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 59. Заказы выше среднего оплаченного чека

*лёгкая* · Диалекты: PostgreSQL, ClickHouse

Финансовый директор хочет увидеть крупные чеки — заказы, сумма которых выше средней суммы среди оплаченных заказов. Среднее нужно считать только по заказам со статусом `paid`: отменённые и другие статусы не должны занижать показатель. Верните `id` заказа и его сумму. Отсортируйте результат по сумме по убыванию.

**Таблицы:**

- **customers**: `id` serial 🔑 — Идентификатор клиента; `name` varchar(100) — Имя клиента; `country` varchar(2) — Страна клиента; `registered_at` date — Дата регистрации
- **products**: `id` serial 🔑 — Идентификатор товара; `name` varchar(100) — Название товара; `category` varchar(50) — Категория товара; `price` numeric(10, 2) — Цена товара
- **orders**: `id` serial 🔑 — Идентификатор заказа; `customer_id` int → customers.id — Идентификатор клиента; `status` varchar(20) — Статус заказа; `total` numeric(10, 2) — Сумма заказа; `created_at` date — Дата создания заказа
- **order_items**: `order_id` int 🔑 — Идентификатор заказа; `product_id` int 🔑 — Идентификатор товара; `quantity` int — Количество товара

**Колонки ответа:** `id`, `total`

**Пример ответа (первые строки):**

| id | total |
|---|---|
| 4 | 8000.00 |
| 8 | 3900.00 |
| 2 | 2500.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/easy-subq-orders-above-avg?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 60. Клиенты, которые уже оформляли заказы

*лёгкая* · Диалекты: PostgreSQL, ClickHouse

Маркетинг хочет разделить клиентскую базу на две группы: тех, кто хотя бы раз дошёл до оформления заказа, и тех, кто только зарегистрировался. Найдите клиентов, у которых есть хотя бы один заказ в таблице `orders`. Статус заказа не важен: учитывайте и оплаченные, и отменённые, и любые другие заказы. Верните `id` и имя клиента. Отсортируйте результат по `id`.

**Таблицы:**

- **customers**: `id` serial 🔑 — Идентификатор клиента; `name` varchar(100) — Имя клиента; `country` varchar(2) — Страна клиента; `registered_at` date — Дата регистрации
- **products**: `id` serial 🔑 — Идентификатор товара; `name` varchar(100) — Название товара; `category` varchar(50) — Категория товара; `price` numeric(10, 2) — Цена товара
- **orders**: `id` serial 🔑 — Идентификатор заказа; `customer_id` int → customers.id — Идентификатор клиента; `status` varchar(20) — Статус заказа; `total` numeric(10, 2) — Сумма заказа; `created_at` date — Дата создания заказа
- **order_items**: `order_id` int 🔑 — Идентификатор заказа; `product_id` int 🔑 — Идентификатор товара; `quantity` int — Количество товара

**Колонки ответа:** `id`, `name`

**Пример ответа (первые строки):**

| id | name |
|---|---|
| 1 | Аня |
| 2 | Боб |
| 3 | Вера |
| 4 | Гриша |
| 5 | Дима |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/easy-subq-customers-with-orders?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 61. Товары без единой продажи

*лёгкая* · Диалекты: PostgreSQL, ClickHouse

Менеджер ассортимента ищет товары, которые завезли в каталог, но за всё время никто так и не купил. Такие позиции можно отправить в распродажу или снять с витрины. Найдите товары, которые ни разу не встречались в заказанных позициях. Верните `id` и название товара, отсортировав результат по `id`.

**Таблицы:**

- **customers**: `id` serial 🔑 — Идентификатор клиента; `name` varchar(100) — Имя клиента; `country` varchar(2) — Страна клиента; `registered_at` date — Дата регистрации
- **products**: `id` serial 🔑 — Идентификатор товара; `name` varchar(100) — Название товара; `category` varchar(50) — Категория товара; `price` numeric(10, 2) — Цена товара
- **orders**: `id` serial 🔑 — Идентификатор заказа; `customer_id` int → customers.id — Идентификатор клиента; `status` varchar(20) — Статус заказа; `total` numeric(10, 2) — Сумма заказа; `created_at` date — Дата создания заказа
- **order_items**: `order_id` int 🔑 — Идентификатор заказа; `product_id` int 🔑 — Идентификатор товара; `quantity` int — Количество товара

**Колонки ответа:** `id`, `name`

**Пример ответа (первые строки):**

| id | name |
|---|---|
| 9 | Шкаф |
| 10 | Диван |
| 11 | Словарь |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/easy-subq-products-never-ordered?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 62. Количество заказов у каждого клиента

*лёгкая* · Диалекты: PostgreSQL, ClickHouse

Саппорт хочет видеть рядом с каждым клиентом счётчик заказов, чтобы сразу отличать постоянных покупателей от тех, кто только зарегистрировался. Для каждого клиента посчитайте общее количество его заказов любого статуса. Клиенты без заказов тоже должны попасть в результат со значением `0`. Верните `id`, имя клиента и счётчик в колонке `orders_count`. Отсортируйте результат по `id` клиента.

**Таблицы:**

- **customers**: `id` serial 🔑 — Идентификатор клиента; `name` varchar(100) — Имя клиента; `country` varchar(2) — Страна клиента; `registered_at` date — Дата регистрации
- **products**: `id` serial 🔑 — Идентификатор товара; `name` varchar(100) — Название товара; `category` varchar(50) — Категория товара; `price` numeric(10, 2) — Цена товара
- **orders**: `id` serial 🔑 — Идентификатор заказа; `customer_id` int → customers.id — Идентификатор клиента; `status` varchar(20) — Статус заказа; `total` numeric(10, 2) — Сумма заказа; `created_at` date — Дата создания заказа
- **order_items**: `order_id` int 🔑 — Идентификатор заказа; `product_id` int 🔑 — Идентификатор товара; `quantity` int — Количество товара

**Колонки ответа:** `id`, `name`, `orders_count`

**Пример ответа (первые строки):**

| id | name | orders_count |
|---|---|---|
| 1 | Аня | 3 |
| 2 | Боб | 1 |
| 3 | Вера | 2 |
| 4 | Гриша | 1 |
| 5 | Дима | 2 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/easy-subq-order-count-per-customer?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 63. Самый доступный товар в каждой категории

*лёгкая* · Диалекты: PostgreSQL, ClickHouse

Маркетинг запускает акцию «начни знакомство с категорией с самого доступного товара». Для каждой категории найдите товар или товары с минимальной ценой внутри этой категории. Верните `id`, название, категорию и цену таких товаров. Отсортируйте результат по категории.

**Таблицы:**

- **customers**: `id` serial 🔑 — Идентификатор клиента; `name` varchar(100) — Имя клиента; `country` varchar(2) — Страна клиента; `registered_at` date — Дата регистрации
- **products**: `id` serial 🔑 — Идентификатор товара; `name` varchar(100) — Название товара; `category` varchar(50) — Категория товара; `price` numeric(10, 2) — Цена товара
- **orders**: `id` serial 🔑 — Идентификатор заказа; `customer_id` int → customers.id — Идентификатор клиента; `status` varchar(20) — Статус заказа; `total` numeric(10, 2) — Сумма заказа; `created_at` date — Дата создания заказа
- **order_items**: `order_id` int 🔑 — Идентификатор заказа; `product_id` int 🔑 — Идентификатор товара; `quantity` int — Количество товара

**Колонки ответа:** `id`, `name`, `category`, `price`

**Пример ответа (первые строки):**

| id | name | category | price |
|---|---|---|---|
| 4 | Книга | books | 450.00 |
| 11 | Словарь | books | 450.00 |
| 1 | Кружка | home | 350.00 |
| 8 | Йога-коврик | sport | 990.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/easy-subq-cheapest-per-category?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 64. Сканы посылок после watermark

*лёгкая* · Диалекты: PostgreSQL

Ты — дата-инженер логистической платформы. Каждую ночь инкрементальный пайплайн забирает свежие сканирования посылок из таблицы parcel_scans и дозагружает их в хранилище. Позиция последней успешной загрузки (watermark) хранится в таблице etl_state — в строке с source_name = `'parcel_scans'` (в таблице могут быть строки и других источников). Твоя задача — собрать очередную порцию: сканы, которых пайплайн ещё не видел, то есть со временем строго больше watermark. Сканы с неизвестным временем (scan_time IS NULL) считаются ещё не готовыми и в порцию не входят.

Верни столбцы:
- `scan_id` — идентификатор скана;
- `parcel_code` — код посылки;
- `hub_code` — код сортировочного хаба;
- `scan_time` — время скана (timestamp, как в таблице);
- `status` — статус посылки (может быть NULL — выводи как есть).

Сортировка: по scan_time по возрастанию, при равенстве времени — по scan_id по возрастанию. Скан с временем, в точности равным watermark, в результат не входит.

**Таблицы:**

- **etl_state**: `source_name` text 🔑 — Имя источника данных; `last_loaded_at` timestamp — Watermark: время последней успешной загрузки
- **parcel_scans**: `scan_id` int 🔑 — Идентификатор скана; `parcel_code` text — Код посылки; `hub_code` text — Код сортировочного хаба; `scan_time` timestamp — Время сканирования (может быть NULL); `status` text — Статус посылки на момент скана

**Колонки ответа:** `scan_id`, `parcel_code`, `hub_code`, `scan_time`, `status`

**Пример ответа (первые строки):**

| scan_id | parcel_code | hub_code | scan_time | status |
|---|---|---|---|---|
| 8 | PKG-1006 | HUB-MUC | 2025-06-10 12:00:01 | arrived |
| 9 | PKG-1003 | HUB-BER | 2025-06-10 15:20:00 | delivered |
| 10 | PKG-1007 | HUB-HAM | 2025-06-10 18:45:00 | arrived |
| 11 | PKG-1004 | HUB-MUC | 2025-06-11 05:10:00 | sorted |
| 12 | PKG-1008 | HUB-BER | 2025-06-11 08:00:00 | arrived |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/etl-watermark-parcel-scans?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 65. Зрители документалок

*лёгкая* · Диалекты: PostgreSQL

Ты работаешь в стриминговом сервисе ReelFlow. Продюсерская команда запускает новую линейку документальных фильмов и хочет разослать анонс только тем, кому это в принципе интересно: зрителям, которые уже смотрели хотя бы один фильм жанра documentary. История просмотров лежит в watch_history, профили — в viewers.

Собери список получателей рассылки с помощью проверки EXISTS: зритель попадает в список, если у него есть хотя бы одна запись просмотра с жанром `'documentary'`. Каждый зритель должен появиться в списке ровно один раз, сколько бы документалок он ни посмотрел.

Верни столбцы:
- `viewer_id` — id зрителя;
- `viewer_name` — его имя.

Сортировка: viewer_id по возрастанию.

**Таблицы:**

- **viewers**: `id` int 🔑 — Идентификатор зрителя; `full_name` text — Имя зрителя; `country` text — Страна
- **watch_history**: `id` int 🔑 — Идентификатор просмотра; `viewer_id` int — id зрителя; `title` text — Название фильма; `genre` text — Жанр; `watched_on` date — Дата просмотра

**Колонки ответа:** `viewer_id`, `viewer_name`

**Пример ответа (первые строки):**

| viewer_id | viewer_name |
|---|---|
| 1 | Alice Morgan |
| 3 | Chloe Dubois |
| 5 | Emma Stone |
| 9 | Iris Vega |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/lsa-documentary-watchers?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**
