# Оконные функции

[← Ко всем темам](../README.md)

## 74. Паузы между прослушиваниями

*лёгкая* · Диалекты: PostgreSQL

Ты — продуктовый аналитик музыкального стриминга TuneWave. Команда рекомендаций хочет понять, насколько плотно слушатели потребляют треки: короткие паузы означают непрерывное прослушивание плейлиста, длинные — что человек вернулся в приложение заново. У тебя журнал стартов треков play_events: кто и в какой момент нажал Play.

Для каждого события посчитай, сколько минут прошло с предыдущего события того же пользователя. Самое первое событие каждого пользователя в результат не включай — его не с чем сравнивать.

Верни столбцы:
- `user_id` — идентификатор слушателя;
- `played_at` — время старта трека (timestamp, как в таблице);
- `minutes_since_prev` — целое число минут с предыдущего события этого пользователя (все интервалы в данных кратны целой минуте).

Сортировка: user_id по возрастанию, затем played_at по возрастанию. Пользователи с единственным событием в вывод не попадают. Временные метки внутри одного пользователя не повторяются.

**Таблицы:**

- **play_events**: `event_id` integer 🔑 — Уникальный идентификатор события; `user_id` integer — Идентификатор слушателя; `played_at` timestamp — Момент старта трека

**Колонки ответа:** `user_id`, `played_at`, `minutes_since_prev`

**Пример ответа (первые строки):**

| user_id | played_at | minutes_since_prev |
|---|---|---|
| 1 | 2026-05-01 09:03:00 | 3 |
| 1 | 2026-05-01 09:10:00 | 7 |
| 1 | 2026-05-01 10:00:00 | 50 |
| 2 | 2026-05-01 12:45:00 | 45 |
| 2 | 2026-05-01 12:50:00 | 5 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ses-stream-play-gaps?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 75. Флаг начала сессии в интернет-магазине

*лёгкая* · Диалекты: PostgreSQL

Ты — аналитик онлайн-гипермаркета FreshCart. Маркетинг готовит расчёт конверсии «на сессию», и первый шаг — разметить поток просмотров страниц: где заканчивается один визит покупателя и начинается следующий. Правило принято такое: если с предыдущего просмотра того же покупателя прошло СТРОГО больше 30 минут — начинается новая сессия; ровно 30 минут — это ещё та же сессия. Самый первый просмотр покупателя всегда открывает новую сессию.

Разметь каждый просмотр из page_views этим флагом.

Верни столбцы:
- `customer_id` — идентификатор покупателя;
- `viewed_at` — время просмотра (timestamp, как в таблице);
- `is_new_session` — boolean: true, если этим просмотром начинается новая сессия, иначе false.

Сортировка: customer_id по возрастанию, затем viewed_at по возрастанию. В вывод входят ВСЕ просмотры, включая первые. Временные метки внутри одного покупателя не повторяются.

**Таблицы:**

- **page_views**: `view_id` integer 🔑 — Уникальный идентификатор просмотра; `customer_id` integer — Идентификатор покупателя; `viewed_at` timestamp — Момент просмотра страницы

**Колонки ответа:** `customer_id`, `viewed_at`, `is_new_session`

**Пример ответа (первые строки):**

| customer_id | viewed_at | is_new_session |
|---|---|---|
| 1 | 2026-05-03 09:00:00 | True |
| 1 | 2026-05-03 09:10:00 | False |
| 1 | 2026-05-03 09:41:00 | True |
| 1 | 2026-05-03 09:50:00 | False |
| 2 | 2026-05-03 12:00:00 | True |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ses-shop-session-flag?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 76. Операционный баланс необанка

*лёгкая* · Диалекты: PostgreSQL

Ты аналитик казначейства в мобильном необанке. Финансовая команда сверяет, как менялся операционный денежный остаток в течение контрольного периода: в `ledger_entries` лежат отдельные зачисления и списания, а `report_days` задаёт даты, которые обязательно должны попасть в отчёт. Руководителю важно видеть не только итог дня, но и остаток, накопленный с начала периода.

Для каждой даты из `report_days` рассчитай чистое изменение: `credit` увеличивает сумму, `debit` уменьшает её. Операции за пределами календаря отчёта не включай. До первой даты отчёта остаток считается равным `0.00`.

**Верни столбцы:**
- `report_date` — дата отчёта, формат `YYYY-MM-DD`;
- `daily_net_usd` — чистое изменение за дату в USD, числовое значение с 2 знаками после запятой;
- `running_balance_usd` — накопленный остаток от первой даты отчёта до текущей включительно, числовое значение с 2 знаками после запятой.

Выведи ровно одну строку на каждую дату из `report_days`. Отсортируй результат по `report_date` по возрастанию. `NULL` в `amount_usd` не участвует в сумме; если на дату нет ни одной операции с известной суммой, `daily_net_usd` должен быть `0.00`. Все отдельные записи одной даты учитываются, даже если их суммы совпадают; после дневного объединения одинаковых дат в результате быть не должно.

**Таблицы:**

- **report_days**: `report_date` date 🔑 — Дата, обязательная для отчёта
- **ledger_entries**: `entry_id` bigint 🔑 — Идентификатор проводки; `posted_date` date — Дата проводки; `entry_type` varchar(10) — Тип проводки: credit или debit; `amount_usd` numeric(10, 2) — сумма операции, USD

**Колонки ответа:** `report_date`, `daily_net_usd`, `running_balance_usd`

**Пример ответа (первые строки):**

| report_date | daily_net_usd | running_balance_usd |
|---|---|---|
| 2026-04-01 | 1120.00 | 1120.00 |
| 2026-04-02 | -91.00 | 1029.00 |
| 2026-04-03 | 300.00 | 1329.00 |
| 2026-04-04 | -75.00 | 1254.00 |
| 2026-04-05 | -210.00 | 1044.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/wfr-neobank-running-balance?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 77. Доля каждого товара в общей выручке через SUM() OVER ()

*средняя* · Диалекты: PostgreSQL

В «Котомаркете» аналитик хочет видеть выручку каждого товара рядом с **общим итогом** и **долей в процентах** — но при этом НЕ схлопывать строки в одну (как сделал бы `GROUP BY`). Каждая строка таблицы `sales` должна остаться на месте.

Таблица `sales` — отдельные продажи товаров (одна строка = одна продажа).

Напишите запрос, который для **каждой** продажи выводит:

- `product` — название товара;
- `revenue` — выручка по этой продаже;
- `total_revenue` — общая выручка по всем продажам (одно и то же число в каждой строке);
- `pct_of_total` — доля этой продажи в общей выручке в процентах, округлённая до 2 знаков: `revenue * 100.0 / total_revenue`.

Подсказка: это классический контраст «окно vs `GROUP BY`». Общий итог нужен в **каждой** строке без агрегирования набора — используйте оконный агрегат `SUM(revenue) OVER ()` (пустые скобки, без `PARTITION BY` и без `ORDER BY`).

Отсортируйте результат по `revenue` по убыванию, при равенстве — по `product` по возрастанию.

**Таблицы:**

- **sales**: `sale_id` integer 🔑 — Идентификатор продажи (первичный ключ); `product` text — Название товара; `category` text — Категория товара; `revenue` numeric(10,2) — Выручка по этой продаже в рублях

**Колонки ответа:** `product`, `revenue`, `total_revenue`, `pct_of_total`

**Пример ответа (первые строки):**

| product | revenue | total_revenue | pct_of_total |
|---|---|---|---|
| Когтеточка Башня | 12000.00 | 40000.00 | 30.00 |
| Корм Премиум 5кг | 8000.00 | 40000.00 | 20.00 |
| Лежанка Облако | 6000.00 | 40000.00 | 15.00 |
| Туннель Радуга | 5000.00 | 40000.00 | 12.50 |
| Корм Диета 2кг | 4000.00 | 40000.00 | 10.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/gen-m7l1-window-share-of-total?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 78. Зарплаты сотрудников: насколько выше или ниже среднего

*средняя* · Диалекты: PostgreSQL

В «Котомаркете» HR анализирует зарплаты сотрудников магазина. Таблица `staff` содержит сотрудников: `id`, `full_name` (имя), `position` (должность), `salary` (зарплата в рублях).

Нужно для **каждого** сотрудника увидеть его зарплату рядом со средней зарплатой **по всему штату** и понять, насколько его оклад отличается от среднего.

Выведите по одной строке на сотрудника со столбцами:

- `full_name` — имя;
- `position` — должность;
- `salary` — зарплата сотрудника;
- `avg_salary` — средняя зарплата по **всей** таблице, округлённая до 2 знаков (`ROUND(..., 2)`); это число должно быть **одинаковым во всех строках**;
- `diff_from_avg` — разница `salary - avg_salary`, тоже округлённая до 2 знаков (положительная — если сотрудник получает больше среднего, отрицательная — если меньше).

Важно: строки **не схлопываются** — в результате остаётся столько же строк, сколько сотрудников. Среднее посчитайте оконным агрегатом `AVG(salary) OVER ()` — **без** `PARTITION BY` и **без** `GROUP BY`.

Отсортируйте результат по `salary` по убыванию, при равенстве — по `id` по возрастанию.

**Таблицы:**

- **staff**: `id` integer 🔑 — Идентификатор сотрудника (первичный ключ); `full_name` text — Полное имя сотрудника; `position` text — Должность сотрудника (продавец, кладовщик, курьер, менеджер, аналитик); `salary` numeric(10,2) — Зарплата сотрудника в рублях

**Колонки ответа:** `full_name`, `position`, `salary`, `avg_salary`, `diff_from_avg`

**Пример ответа (первые строки):**

| full_name | position | salary | avg_salary | diff_from_avg |
|---|---|---|---|---|
| Дарья Пушистова | менеджер | 92000.00 | 57000.00 | 35000.00 |
| Игорь Лапкин | продавец | 61000.00 | 57000.00 | 4000.00 |
| Анна Котова | продавец | 58000.00 | 57000.00 | 1000.00 |
| Светлана Барсикова | продавец | 57000.00 | 57000.00 | 0.00 |
| Павел Когтев | кладовщик | 52000.00 | 57000.00 | -5000.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/gen-m7l1b-staff-salary-vs-average?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 79. Рейтинг студентов по средней оценке внутри специальности

*средняя* · Диалекты: PostgreSQL, ClickHouse

Учебный отдел хочет составить рейтинг сильных студентов в разрезе специальностей. Для каждого студента посчитайте его среднюю оценку как `ROUND(AVG(grades.grade_value), 2)` (столбец `avg_grade`) и оставьте только тех, у кого средняя оценка строго больше `3.5`. Внутри каждой специальности (`majors.major_id`) проставьте каждому студенту уникальный порядковый номер `rank_in_major`: используйте оконную функцию `ROW_NUMBER()` с `PARTITION BY majors.major_id`, упорядочивая студентов по средней оценке по убыванию. Это именно сквозная нумерация (1, 2, 3, ...), а не разделяемый ранг: студенты с одинаковой средней оценкой всё равно получают разные подряд идущие номера. Чтобы при равенстве средних оценок результат был детерминированным, в `ORDER BY` оконной функции добавьте тай-брейк по `students.student_id` по возрастанию. Выведите столбцы `student_id`, `student_name`, `major_name`, `avg_grade`, `rank_in_major` и отсортируйте итог по `major_name`, а внутри специальности — по `avg_grade` по убыванию.

**Таблицы:**

- **majors**: `major_id` serial 🔑 — Идентификатор специальности; `major_name` varchar(100) — Название специальности
- **students**: `student_id` serial 🔑 — Идентификатор студента; `student_name` varchar(100) — Имя студента; `major_id` integer → majors.major_id — Идентификатор специальности
- **courses**: `course_id` serial 🔑 — Идентификатор курса; `course_name` varchar(100) — Название курса
- **grades**: `grade_id` serial 🔑 — Идентификатор оценки; `student_id` integer → students.student_id — Идентификатор студента; `course_id` integer → courses.course_id — Идентификатор курса; `grade_value` decimal(3,2) — Значение оценки

**Колонки ответа:** `student_id`, `student_name`, `major_name`, `avg_grade`, `rank_in_major`

**Пример ответа (первые строки):**

| student_id | student_name | major_name | avg_grade | rank_in_major |
|---|---|---|---|---|
| 1 | Alice Johnson | Computer Science | 4.25 | 1 |
| 2 | Bob Smith | Computer Science | 3.65 | 2 |
| 3 | Carol White | Mathematics | 4.05 | 1 |
| 5 | Elena Petrova | Physics | 4.05 | 1 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1778004364778-0tho?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 80. Урожайность по сортам культур с рангированием

*средняя* · Диалекты: PostgreSQL

Сельскохозяйственная компания хочет проанализировать эффективность разных сортов культур. Найти все сорта культур, которые выращиваются на нескольких участках (минимум 2), и вывести для каждого сорта общую площадь посева, средний урожай за все участки этого сорта, общее количество участков, а также ранг каждого сорта по средней урожайности (урожай на единицу площади в килограммах на гектар). Результаты отсортировать по среднему урожаю на гектар в порядке убывания, затем по названию сорта в алфавитном порядке.

**Таблицы:**

- **crop_varieties**: `variety_id` serial 🔑; `variety_name` varchar(100); `crop_type` varchar(50)
- **farm_plots**: `plot_id` serial 🔑; `plot_name` varchar(100); `area_hectares` decimal(10,2); `variety_id` integer → crop_varieties.variety_id
- **harvest_records**: `record_id` serial 🔑; `plot_id` integer → farm_plots.plot_id; `harvest_year` integer; `harvest_kg` decimal(12,2)
- **weather_data**: `weather_id` serial 🔑; `plot_id` integer → farm_plots.plot_id; `weather_year` integer; `rainfall_mm` decimal(8,2)

**Колонки ответа:** `variety_name`, `total_area_hectares`, `avg_harvest_kg`, `plot_count`, `yield_rank`

**Пример ответа (первые строки):**

| variety_name | total_area_hectares | avg_harvest_kg | plot_count | yield_rank |
|---|---|---|---|---|
| Amber Barley | 33.20 | 2952.3333333333333333 | 3 | 1 |
| Golden Wheat | 46.55 | 3103.6666666666666667 | 3 | 2 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1786790300439-tv0i?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 81. Читатели-рекордсмены по жанрам

*сложная* · Диалекты: PostgreSQL

Библиотечная сеть анализирует активность читателей по жанрам книг, чтобы выявить самых заметных посетителей в каждом направлении.

Нужно рассмотреть только выдачи, которые уже завершены возвратом книги (дата возврата заполнена), и для каждого жанра посчитать суммарное число выданных страниц для каждого читателя (сумма page_count всех книг, которые он брал в этом жанре).

В каждом жанре присвоить читателям место по убыванию этой суммы: при равных значениях места не пропускаются (одинаковый ранг для равных сумм, следующий ранг идёт подряд без пропуска). Оставить только читателей, занявших первое место в своём жанре, и вывести жанр (genre), имя читателя (reader_name), суммарное количество страниц (total_pages). Отсортировать результат по жанру по алфавиту, а при совпадении жанра — по убыванию total_pages.

**Таблицы:**

- **authors**: `author_id` serial 🔑; `full_name` varchar(100)
- **genres**: `genre_id` serial 🔑; `genre_name` varchar(50)
- **books**: `book_id` serial 🔑; `title` varchar(150); `author_id` integer → authors.author_id; `genre_id` integer → genres.genre_id; `page_count` integer
- **readers**: `reader_id` serial 🔑; `full_name` varchar(100); `city` varchar(50)
- **library_branches**: `branch_id` serial 🔑; `branch_name` varchar(100); `address` varchar(150)
- **loans**: `loan_id` serial 🔑; `book_id` integer → books.book_id; `reader_id` integer → readers.reader_id; `branch_id` integer → library_branches.branch_id; `loan_date` date; `return_date` date

**Колонки ответа:** `genre`, `reader_name`, `total_pages`

**Пример ответа (первые строки):**

| genre | reader_name | total_pages |
|---|---|---|
| Classic Literature | Elena Petrova | 1200 |
| Fantasy | Ivan Sokolov | 820 |
| Mystery | Olga Volkova | 380 |
| Science Fiction | Sarah Connor | 600 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1790350306207-8sq5?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 82. Динамика выплат по страховым полисам

*сложная* · Диалекты: PostgreSQL

Страховая компания хранит информацию о полисах клиентов и поданных по ним claims (страховых случаях). Нужно проанализировать только claims со статусом 'approved' (одобренные) и суммой выплаты больше 0.

**Таблицы:**

- **policies**: `policy_id` serial 🔑; `policy_holder` varchar(100); `policy_type` varchar(50); `start_date` date; `monthly_premium` decimal(10,2)
- **claims**: `claim_id` serial 🔑; `policy_id` integer → policies.policy_id; `claim_date` date; `status` varchar(20); `payout_amount` decimal(10,2)

**Колонки ответа:** `policy_holder`, `policy_type`, `claim_date`, `payout_amount`, `claim_seq`, `prev_payout`, `running_total`

**Пример ответа (первые строки):**

| policy_holder | policy_type | claim_date | payout_amount | claim_seq | prev_payout | running_total |
|---|---|---|---|---|---|---|
| Anna Kowalski | Auto | 2022-02-14 | 700.00 | 1 | NULL | 700.00 |
| Anna Kowalski | Auto | 2022-11-11 | 950.00 | 2 | 700.00 | 1650.00 |
| Carlos Mendez | Health | 2023-01-20 | 4500.00 | 1 | NULL | 4500.00 |
| David Chen | Home | 2021-10-05 | 1800.00 | 1 | NULL | 1800.00 |
| David Chen | Home | 2022-12-25 | 600.00 | 2 | 1800.00 | 2400.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1790535919225-byut?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 83. Динамика платежей участников фитнес-клуба

*сложная* · Диалекты: PostgreSQL

Сеть фитнес-клубов хочет понять, как меняются платежи постоянных клиентов от месяца к месяцу, чтобы выявлять тех, кто снижает активность подписки.

**Таблицы:**

- **clubs**: `club_id` serial 🔑; `club_name` varchar(100); `city` varchar(100)
- **trainers**: `trainer_id` serial 🔑; `full_name` varchar(100); `club_id` integer → clubs.club_id
- **membership_plans**: `plan_id` serial 🔑; `plan_name` varchar(100); `monthly_price` decimal(10,2)
- **members**: `member_id` serial 🔑; `full_name` varchar(100); `club_id` integer → clubs.club_id; `trainer_id` integer → trainers.trainer_id; `join_date` date
- **subscriptions**: `subscription_id` serial 🔑; `member_id` integer → members.member_id; `plan_id` integer → membership_plans.plan_id; `start_date` date; `end_date` date
- **payments**: `payment_id` serial 🔑; `subscription_id` integer → subscriptions.subscription_id; `payment_date` date; `amount` decimal(10,2)

**Колонки ответа:** `member_name`, `payment_date`, `payment_amount`, `previous_amount`, `amount_change`

**Пример ответа (первые строки):**

| member_name | payment_date | payment_amount | previous_amount | amount_change |
|---|---|---|---|---|
| Natalia Belova | 2023-07-01 | 40.00 | 70.00 | -30.00 |
| Oleg Titov | 2023-03-01 | 20.00 | 45.00 | -25.00 |
| Ivan Sokolov | 2023-05-01 | 50.00 | 70.00 | -20.00 |
| Elena Petrova | 2023-04-01 | 30.00 | 45.00 | -15.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1790360193402-040t?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 84. Прирост выручки автопарка по месяцам

*сложная* · Диалекты: PostgreSQL

Сеть проката автомобилей хочет понять, как меняется выручка по каждой локации от месяца к месяцу.

**Таблицы:**

- **locations**: `location_id` serial 🔑; `city` varchar(100); `branch_name` varchar(100)
- **cars**: `car_id` serial 🔑; `location_id` integer → locations.location_id; `make` varchar(50); `model` varchar(50); `daily_rate` decimal(10,2)
- **customers**: `customer_id` serial 🔑; `full_name` varchar(100); `email` varchar(100); `phone` varchar(30)
- **employees**: `employee_id` serial 🔑; `location_id` integer → locations.location_id; `full_name` varchar(100); `position` varchar(50)
- **bookings**: `booking_id` serial 🔑; `customer_id` integer → customers.customer_id; `car_id` integer → cars.car_id; `employee_id` integer → employees.employee_id; `start_date` date; `end_date` date; `status` varchar(20)
- **payments**: `payment_id` serial 🔑; `booking_id` integer → bookings.booking_id; `amount` decimal(10,2); `payment_date` date; `method` varchar(30)

**Колонки ответа:** `branch_name`, `revenue_month`, `total_revenue`, `revenue_change`

**Пример ответа (первые строки):**

| branch_name | revenue_month | total_revenue | revenue_change |
|---|---|---|---|
| Almaty Central | 2024-01-01 | 330.00 | 0.00 |
| Almaty Central | 2024-02-01 | 400.00 | 70.00 |
| Almaty Central | 2024-03-01 | 360.00 | -40.00 |
| Astana North | 2024-01-01 | 360.00 | 0.00 |
| Astana North | 2024-02-01 | 352.00 | -8.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1790361107661-qhhp?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 85. Кассовые рекорды кинозала по месяцам

*сложная* · Диалекты: PostgreSQL

Сеть кинотеатров хочет понять динамику сборов по каждому фильму в разрезе месяцев показа.

**Таблицы:**

- **genres**: `genre_id` serial 🔑; `genre_name` varchar(50)
- **films**: `film_id` serial 🔑; `title` varchar(150); `genre_id` integer → genres.genre_id; `release_year` integer
- **halls**: `hall_id` serial 🔑; `hall_name` varchar(50); `capacity` integer
- **screenings**: `screening_id` serial 🔑; `film_id` integer → films.film_id; `hall_id` integer → halls.hall_id; `show_date` date; `show_time` varchar(10)
- **customers**: `customer_id` serial 🔑; `full_name` varchar(100); `email` varchar(100)
- **tickets**: `ticket_id` serial 🔑; `screening_id` integer → screenings.screening_id; `customer_id` integer → customers.customer_id; `price` decimal(6,2); `purchase_date` date

**Колонки ответа:** `title`, `revenue_month`, `revenue`, `change_vs_prev_month`

**Пример ответа (первые строки):**

| title | revenue_month | revenue | change_vs_prev_month |
|---|---|---|---|
| Stellar Horizon | 2024-02-01 | 60.00 | 15.00 |
| Quiet Autumn | 2024-02-01 | 17.00 | 9.00 |
| Laugh Track | 2024-02-01 | 15.00 | 8.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1790478543031-ofx6?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 86. Восходящие звёзды тревел-агентства

*сложная* · Диалекты: PostgreSQL

Агентство «南Полюс Трэвел» продаёт туры через сеть гидов, и руководство хочет понять, чьи продажи растут быстрее всего от квартала к кварталу.

**Таблицы:**

- **guides**: `guide_id` serial 🔑; `full_name` varchar(100); `hire_date` date
- **destinations**: `destination_id` serial 🔑; `country` varchar(100); `city` varchar(100)
- **tours**: `tour_id` serial 🔑; `tour_name` varchar(150); `destination_id` integer → destinations.destination_id; `base_price` decimal(10,2); `duration_days` integer
- **customers**: `customer_id` serial 🔑; `full_name` varchar(100); `email` varchar(150)
- **bookings**: `booking_id` serial 🔑; `customer_id` integer → customers.customer_id; `tour_id` integer → tours.tour_id; `guide_id` integer → guides.guide_id; `booking_date` date; `total_amount` decimal(10,2); `status` varchar(20)
- **payments**: `payment_id` serial 🔑; `booking_id` integer → bookings.booking_id; `payment_date` date; `amount` decimal(10,2)
- **reviews**: `review_id` serial 🔑; `booking_id` integer → bookings.booking_id; `rating` integer

**Колонки ответа:** `guide_name`, `sale_year`, `sale_quarter`, `quarter_revenue`, `growth_pct`, `growth_rank`

**Пример ответа (первые строки):**

| guide_name | sale_year | sale_quarter | quarter_revenue | growth_pct | growth_rank |
|---|---|---|---|---|---|
| Anna Kowalski | 2023 | 2 | 700.00 | 100.00 | 1 |
| Marco Rossi | 2023 | 3 | 790.00 | 92.68 | 2 |
| Elena Petrova | 2023 | 4 | 700.00 | 84.21 | 3 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1790481334663-qe95?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 87. Динамика повторных визитов пациентов к врачам

*сложная* · Диалекты: PostgreSQL

Клиника анализирует нагрузку врачей и повторные обращения пациентов по отделениям. Для каждого приёма нужно понять, сколько дней прошло с предыдущего визита того же пациента к тому же врачу, чтобы выявить частых посетителей.

Учитываются только приёмы со статусом 'completed'. Для каждого врача посчитайте среднее количество дней между последовательными визитами одного и того же пациента (без учёта первого визита пациента, у которого нет предыдущего), округлив до 2 знаков после запятой. В расчёт включайте только врачей, у которых есть хотя бы 2 таких интервала (то есть минимум 2 повторных визита в сумме по всем пациентам).

Выведите имя врача (doctor_name), название отделения (department_name) и среднее количество дней между визитами (avg_days_between). Отсортируйте результат по среднему количеству дней от меньшего к большему, при равенстве — по имени врача по возрастанию.

**Таблицы:**

- **departments**: `department_id` serial 🔑; `department_name` varchar(100)
- **doctors**: `doctor_id` serial 🔑; `full_name` varchar(100); `department_id` integer → departments.department_id
- **patients**: `patient_id` serial 🔑; `full_name` varchar(100); `birth_date` date
- **rooms**: `room_id` serial 🔑; `room_number` varchar(10); `department_id` integer → departments.department_id
- **appointments**: `appointment_id` serial 🔑; `patient_id` integer → patients.patient_id; `doctor_id` integer → doctors.doctor_id; `room_id` integer → rooms.room_id; `appointment_date` date; `status` varchar(20)
- **diagnoses**: `diagnosis_id` serial 🔑; `appointment_id` integer → appointments.appointment_id; `diagnosis_code` varchar(10); `description` text
- **prescriptions**: `prescription_id` serial 🔑; `appointment_id` integer → appointments.appointment_id; `medication` varchar(100); `dosage` varchar(50)

**Колонки ответа:** `doctor_name`, `department_name`, `avg_days_between`

**Пример ответа (первые строки):**

| doctor_name | department_name | avg_days_between |
|---|---|---|
| Dr. Anna Ivanova | Cardiology | 16.75 |
| Dr. Mikhail Sokolov | Neurology | 31.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1789731153744-4c8k?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**
