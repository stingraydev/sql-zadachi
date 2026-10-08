# CTE (WITH) — общие табличные выражения

[← Ко всем темам](../README.md)

## 66. Топовые клиенты банка по сумме транзакций

*сложная* · Диалекты: PostgreSQL

Банк ранжирует активных клиентов по сумме транзакций за последние 12 месяцев. Найдите клиентов, у которых суммарная сумма транзакций по их счетам за этот период (`SUM(transactions.amount)`) превышает `10000`. Для каждого выведите `client_id`, имя клиента (`client_name`), общую сумму (`total_amount`) и категорию активности (`activity_category`): `high`, если сумма больше `20000`, иначе `medium`. Отсортируйте по убыванию суммы, при равенстве — по `client_id`.

**Таблицы:**

- **clients**: `id` serial 🔑 — Идентификатор клиента; `name` varchar(100) — Имя клиента; `registration_date` date — Дата регистрации
- **accounts**: `id` serial 🔑 — Идентификатор счёта; `client_id` integer → clients.id — Идентификатор клиента; `balance` decimal(15,2) — Баланс счёта
- **transactions**: `id` serial 🔑 — Идентификатор транзакции; `account_id` integer → accounts.id — Идентификатор счёта; `transaction_date` timestamp — Дата и время транзакции; `amount` decimal(15,2) — Сумма транзакции; `transaction_type` varchar(50) — Тип транзакции

**Колонки ответа:** `client_id`, `client_name`, `total_amount`, `activity_category`

**Пример ответа (первые строки):**

| client_id | client_name | total_amount | activity_category |
|---|---|---|---|
| 2 | Светлана Петрова | 27000.00 | high |
| 5 | Николай Сидоров | 27000.00 | high |
| 1 | Иван Иванов | 13000.00 | medium |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1777242925149-2xrk?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 67. Поквартальная эффективность менеджеров продаж

*сложная* · Диалекты: PostgreSQL

Руководство компании готовит квартальный отчёт по эффективности менеджеров отдела `Sales` (`departments.name = 'Sales'`). Рассматривайте только сотрудников этого отдела: для каждого менеджера и каждого квартала (по `EXTRACT(QUARTER FROM sales.sale_date)`) посчитайте суммарную сумму его продаж за квартал (`SUM(sales.amount)`) и оставьте только тех менеджеров, у кого эта квартальная сумма больше `50000`. Из этих квалифицированных менеджеров отдела `Sales` и формируется итоговый набор, и все расчёты ведутся внутри него. Для каждой строки выведите: имя менеджера (`first_name || ' ' || last_name`), квартал, его квартальную сумму продаж, процент `percentage_of_total` — долю квартальной суммы менеджера от суммарных продаж всех квалифицированных менеджеров отдела `Sales` за этот же квартал (то есть от суммы по отобранному набору, а НЕ от всех продаж компании), округлённый до 2 знаков, место менеджера в квартальном рейтинге по объёму продаж (`RANK()` с разбиением по кварталу и сортировкой по сумме по убыванию, где `1` — лучший результат), а также сумму продаж лучшего менеджера в этом же квартале (`top_manager_sales`). Отсортируйте результат по кварталу, затем по месту менеджера в рейтинге.

**Таблицы:**

- **departments**: `id` serial 🔑 — Идентификатор отдела; `name` varchar(100) — Название отдела
- **employees**: `id` serial 🔑 — Идентификатор сотрудника; `first_name` varchar(50) — Имя сотрудника; `last_name` varchar(50) — Фамилия сотрудника; `department_id` integer → departments.id — Идентификатор отдела; `hire_date` date — Дата приёма на работу
- **customers**: `id` serial 🔑 — Идентификатор клиента; `company_name` varchar(100) — Название компании; `contact_person` varchar(100) — Контактное лицо; `registration_date` date — Дата регистрации
- **sales**: `id` serial 🔑 — Идентификатор продажи; `employee_id` integer → employees.id — Идентификатор сотрудника; `customer_id` integer → customers.id — Идентификатор клиента; `sale_date` date — Дата продажи; `amount` decimal(10,2) — Сумма продажи

**Колонки ответа:** `manager_name`, `quarter`, `quarterly_amount`, `percentage_of_total`, `manager_rank`, `top_manager_sales`

**Пример ответа (первые строки):**

| manager_name | quarter | quarterly_amount | percentage_of_total | manager_rank | top_manager_sales |
|---|---|---|---|---|---|
| Michael Smith | 1 | 131000.00 | 43.23 | 1 | 131000.00 |
| Anna Peterson | 1 | 120000.00 | 39.60 | 2 | 131000.00 |
| Daniel Wolf | 1 | 52000.00 | 17.16 | 3 | 131000.00 |
| Anna Peterson | 2 | 120000.00 | 34.19 | 1 | 120000.00 |
| Michael Smith | 2 | 84000.00 | 23.93 | 2 | 120000.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1775635598933-m421?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 68. Топ курьеры по доставкам с учётом срочности

*сложная* · Диалекты: PostgreSQL

Логистическая команда анализирует работу курьеров и хочет выделить тех, кто выполнял и срочные, и обычные доставки. Учитывайте только доставки с `delivery_time` от `2024-12-01` включительно и только курьеров, у которых таких доставок больше одной. Сначала определите место каждого такого курьера по количеству доставок: наибольшее количество получает первое место, а при равенстве места делятся и следующее место пропускается (1, 1, 3). Места считаются среди ВСЕХ курьеров с более чем одной доставкой, даже если курьер не попадёт в итоговый список. Затем оставьте только тех, у кого есть хотя бы одна срочная (`is_urgent = true`) и хотя бы одна обычная доставка — их места при этом не пересчитываются. Выведите пять колонок: `courier_name` — имя курьера, `total_deliveries` — количество его доставок, `urgent_deliveries` — сколько из них срочных, `urgent_percentage` — долю срочных в процентах, округлённую до одного знака после запятой, и `delivery_rank` — это место. Отсортируйте результат по месту.

**Таблицы:**

- **regions**: `region_id` serial 🔑 — Идентификатор региона; `region_name` varchar(100) — Название региона; `region_code` varchar(10) — Код региона
- **warehouses**: `warehouse_id` serial 🔑 — Идентификатор склада; `warehouse_name` varchar(100) — Название склада; `region_id` integer → regions.region_id — Идентификатор региона; `address` varchar(200) — Адрес склада
- **customers**: `customer_id` serial 🔑 — Идентификатор клиента; `customer_name` varchar(100) — Имя клиента; `phone` varchar(20) — Телефон клиента; `email` varchar(100) — Электронная почта клиента; `region_id` integer → regions.region_id — Идентификатор региона
- **couriers**: `courier_id` serial 🔑 — Идентификатор курьера; `courier_name` varchar(100) — Имя курьера; `phone` varchar(20) — Телефон курьера; `hire_date` date — Дата приёма на работу; `region_id` integer → regions.region_id — Идентификатор региона
- **vehicles**: `vehicle_id` serial 🔑 — Идентификатор транспорта; `courier_id` integer → couriers.courier_id — Идентификатор курьера; `vehicle_type` varchar(50) — Тип транспорта; `license_plate` varchar(20) — Государственный номер
- **package_types**: `type_id` serial 🔑 — Идентификатор типа посылки; `type_name` varchar(50) — Название типа посылки; `base_cost` decimal(8,2) — Базовая стоимость
- **orders**: `order_id` serial 🔑 — Идентификатор заказа; `customer_id` integer → customers.customer_id — Идентификатор клиента; `warehouse_id` integer → warehouses.warehouse_id — Идентификатор склада; `order_date` timestamp — Дата и время заказа; `is_urgent` boolean — Признак срочности; `total_amount` decimal(10,2) — Сумма заказа
- **packages**: `package_id` serial 🔑 — Идентификатор посылки; `order_id` integer → orders.order_id — Идентификатор заказа; `type_id` integer → package_types.type_id — Идентификатор типа посылки; `weight` decimal(6,2) — Вес посылки; `dimensions` varchar(50) — Габариты посылки
- **deliveries**: `delivery_id` serial 🔑 — Идентификатор доставки; `order_id` integer → orders.order_id — Идентификатор заказа; `courier_id` integer → couriers.courier_id — Идентификатор курьера; `pickup_time` timestamp — Время забора посылки; `delivery_time` timestamp — Время доставки; `status` varchar(20) — Статус доставки
- **delivery_routes**: `route_id` serial 🔑 — Идентификатор маршрута; `courier_id` integer → couriers.courier_id — Идентификатор курьера; `route_date` date — Дата маршрута; `total_distance` decimal(8,2) — Общая дистанция

**Колонки ответа:** `courier_name`, `total_deliveries`, `urgent_deliveries`, `urgent_percentage`, `delivery_rank`

**Пример ответа (первые строки):**

| courier_name | total_deliveries | urgent_deliveries | urgent_percentage | delivery_rank |
|---|---|---|---|---|
| Олег Кузнецов | 2 | 1 | 50.0 | 1 |
| Сергей Николаев | 2 | 1 | 50.0 | 1 |
| Игорь Сидоров | 2 | 1 | 50.0 | 1 |
| Александр Петров | 2 | 1 | 50.0 | 1 |
| Максим Федоров | 2 | 1 | 50.0 | 1 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1777263423404-9c2a?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 69. Топ-3 сотрудников по суммарному доходу в каждом отделе

*сложная* · Диалекты: PostgreSQL

Финансовый отдел готовит расширенный отчёт по доходам сотрудников с учётом оклада, бонусов, продаж и удержаний. По таблицам `employees`, `departments`, `bonuses`, `sales` и `deductions` определите суммарный доход каждого сотрудника по формуле: `salary + SUM(bonus) + SUM(sales.amount) - SUM(deductions.amount)`. Для каждого отдела верните трёх сотрудников с наибольшим суммарным доходом. Выведите `department_name`, `employee_name` и `total_revenue`. Отсортируйте результат по `department_name`, затем по `total_revenue` по убыванию.

**Таблицы:**

- **departments**: `id` serial 🔑 — Идентификатор отдела; `name` varchar(100) — Название отдела
- **employees**: `id` serial 🔑 — Идентификатор сотрудника; `name` varchar(100) — Имя сотрудника; `department_id` integer → departments.id — Идентификатор отдела; `salary` decimal(10, 2) — Оклад сотрудника
- **bonuses**: `id` serial 🔑 — Идентификатор премии; `employee_id` integer → employees.id — Идентификатор сотрудника; `bonus` decimal(10, 2) — Сумма премии; `date` date — Дата премии
- **sales**: `id` serial 🔑 — Идентификатор продажи; `employee_id` integer → employees.id — Идентификатор сотрудника; `amount` decimal(10, 2) — Сумма продажи; `sale_date` date — Дата продажи
- **deductions**: `id` serial 🔑 — Идентификатор удержания; `employee_id` integer → employees.id — Идентификатор сотрудника; `amount` decimal(10, 2) — Сумма удержания; `date` date — Дата удержания

**Колонки ответа:** `department_name`, `employee_name`, `total_revenue`

**Пример ответа (первые строки):**

| department_name | employee_name | total_revenue |
|---|---|---|
| Finance | Heidi | 70000.00 |
| Finance | Grace | 65000.00 |
| Finance | Frank | 60000.00 |
| HR | Dave | 61500.00 |
| HR | Eve | 51000.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1775671119763-2ukv?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 70. Хиты месяца по новым трекам в плейлистах

*сложная* · Диалекты: PostgreSQL

Музыкальная команда смотрит на свежие добавления в плейлисты и хочет понять, у каких из них больше всего прослушиваний за всё время. Возьмите треки, которые были добавлены в плейлисты за последний месяц (то есть `playlist_tracks.added_at >= NOW() - INTERVAL '1 month'`), и для каждого такого трека посчитайте суммарное число его прослушиваний из таблицы `track_plays` за всю историю (а не только за последний месяц). Для каждого трека выведите его название (`tracks.title`), имя исполнителя (`artists.name` как `artist_name`) и общее количество прослушиваний (`play_count`). Отсортируйте результат по `play_count` по убыванию и оставьте топ-10 треков.

**Таблицы:**

- **tracks**: `id` serial 🔑 — Идентификатор трека; `title` varchar(100) — Название трека; `artist_id` integer → artists.id — Идентификатор исполнителя; `duration` integer — Длительность трека
- **artists**: `id` serial 🔑 — Идентификатор исполнителя; `name` varchar(100) — Имя исполнителя
- **playlists**: `id` serial 🔑 — Идентификатор плейлиста; `name` varchar(100) — Название плейлиста; `created_at` timestamp — Дата создания
- **playlist_tracks**: `playlist_id` integer → playlists.id — Идентификатор плейлиста; `track_id` integer → tracks.id — Идентификатор трека; `added_at` timestamp — Дата добавления
- **track_plays**: `track_id` integer → tracks.id — Идентификатор трека; `play_date` timestamp — Дата прослушивания

**Колонки ответа:** `title`, `artist_name`, `play_count`

**Пример ответа (первые строки):**

| title | artist_name | play_count |
|---|---|---|
| Track 1 | Artist 1 | 3 |
| Track 2 | Artist 2 | 3 |
| Track 3 | Artist 3 | 1 |
| Track 4 | Artist 1 | 1 |
| Track 5 | Artist 2 | 1 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1775675622104-qs7d?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 71. Топ-5 самых прослушиваемых артистов в плейлистах

*сложная* · Диалекты: PostgreSQL

Музыкальный сервис считает, какие артисты чаще всего звучат в плейлистах. Каждое прослушивание плейлиста (`plays`) засчитывается всем артистам, чьи треки входят в этот плейлист. Учитывайте только плейлисты, созданные более 30 дней назад (`playlists.created_at`), и прослушивания за последний месяц (`plays.play_date`). Найдите топ-5 артистов по числу таких прослушиваний: выведите имя артиста (`name`) и количество прослушиваний (`total_plays`), отсортировав по убыванию, при равенстве — по имени.

**Таблицы:**

- **artists**: `id` serial 🔑 — Идентификатор исполнителя; `name` varchar(100) — Имя исполнителя
- **tracks**: `id` serial 🔑 — Идентификатор трека; `artist_id` integer → artists.id — Идентификатор исполнителя; `title` varchar(100) — Название трека
- **playlists**: `id` serial 🔑 — Идентификатор плейлиста; `name` varchar(100) — Название плейлиста; `created_at` timestamp — Дата создания
- **playlist_tracks**: `playlist_id` integer → playlists.id — Идентификатор плейлиста; `track_id` integer → tracks.id — Идентификатор трека
- **plays**: `playlist_id` integer → playlists.id — Идентификатор плейлиста; `play_date` timestamp — Дата прослушивания

**Колонки ответа:** `name`, `total_plays`

**Пример ответа (первые строки):**

| name | total_plays |
|---|---|
| Artist A | 2 |
| Artist C | 2 |
| Artist D | 2 |
| Artist B | 1 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1775675459674-b6li?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 72. Рейтинг успеваемости студентов по кафедрам с динамикой оценок

*сложная* · Диалекты: PostgreSQL

В университете нужно выявить лучших студентов каждой кафедры, которые улучшили свои оценки за последний семестр. Найдите студентов, у которых средняя оценка за текущий семестр выше средней за предыдущий, и определите для каждого студента: его имя, кафедру, среднюю оценку в текущем семестре, улучшение оценки (разница), а также его рейтинг в своей кафедре по величине улучшения (с наибольшего улучшения на наименьшее). Выведите только студентов, чьё улучшение составило не менее 0.5 балла, отсортировав результат по кафедре, затем по рейтингу в кафедре.

**Таблицы:**

- **departments**: `dept_id` serial 🔑; `dept_name` varchar(100)
- **students**: `student_id` serial 🔑; `student_name` varchar(100); `dept_id` integer → departments.dept_id
- **semesters**: `semester_id` serial 🔑; `semester_name` varchar(50); `year` integer
- **grades**: `grade_id` serial 🔑; `student_id` integer → students.student_id; `semester_id` integer → semesters.semester_id; `grade_value` decimal(3, 2)

**Колонки ответа:** `student_name`, `dept_name`, `current_avg`, `improvement`, `dept_rank`

**Пример ответа (первые строки):**

| student_name | dept_name | current_avg | improvement | dept_rank |
|---|---|---|---|---|
| Alice Johnson | Computer Science | 4.10 | 0.60 | 1 |
| Charlie Brown | Mathematics | 4.20 | 0.60 | 1 |
| Eve Wilson | Physics | 4.10 | 0.80 | 1 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1788857992408-sa5x?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 73. Рост выручки месяц к месяцу

*сложная* · Диалекты: PostgreSQL

Финансовая команда отслеживает динамику выручки по месяцам. Для каждого месяца вычислите месячную выручку, выручку предыдущего месяца и процент роста относительно предыдущего месяца. Выведите `month`, `revenue`, `prev_revenue` и `growth_pct`, округлив `growth_pct` до 2 знаков после запятой.

**Таблицы:**

- **transactions**: `id` int 🔑 — Идентификатор транзакции; `amount` decimal — Сумма транзакции; `created_at` date — Дата транзакции

**Колонки ответа:** `month`, `revenue`, `prev_revenue`, `growth_pct`

**Пример ответа (первые строки):**

| month | revenue | prev_revenue | growth_pct |
|---|---|---|---|
| 2024-01-01 | 450.00 | NULL | NULL |
| 2024-02-01 | 550.00 | 450.00 | 22.22 |
| 2024-03-01 | 700.00 | 550.00 | 27.27 |
| 2024-04-01 | 850.00 | 700.00 | 21.43 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1775673452252-fuqx?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**
