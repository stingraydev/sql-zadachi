# JOIN — соединение таблиц

[← Ко всем темам](../README.md)

## 39. Полки второго уровня

*лёгкая* · Диалекты: PostgreSQL

Ты — аналитик каталога в крупном маркетплейсе. Категории товаров хранятся деревом: у каждой категории может быть родительская, у корневых разделов родителя нет. Команда витрины переделывает страницу раздела «Electronics» и просит список только его ПРЯМЫХ подкатегорий — внуков и более глубокие уровни показывать нельзя, они уедут на свои страницы.

Таблица categories: id, name, parent_id (NULL у корневых разделов). Название раздела ровно `'Electronics'`.

Верни столбцы:
- `subcategory_name` — название прямой подкатегории раздела `'Electronics'` (текст, как в таблице).

Сортировка: по subcategory_name по возрастанию (алфавит). Категории других разделов и любые категории глубже первого уровня вложенности в вывод не попадают. Дубликатов имён среди прямых детей нет.

**Таблицы:**

- **categories**: `id` int 🔑 — Идентификатор категории; `name` text — Название категории; `parent_id` int — Родительская категория (NULL у корневых)

**Колонки ответа:** `subcategory_name`

**Пример ответа (первые строки):**

| subcategory_name |
|---|
| Audio |
| Cameras |
| Laptops |
| Phones |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/rct-store-direct-subcategories?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 40. Один к одному, один ко многим

*лёгкая* · Диалекты: PostgreSQL

Ты — аналитик онлайн-школы Brightpath. В базе три таблицы: students — по одной строке на ученика; student_profiles — анкета, ровно одна на каждого ученика (связь один к одному); enrollments — записи на курсы: у ученика их может быть несколько, а может не быть вовсе (связь один ко многим). Куратору нужна сводка: на каком тарифе учится каждый ученик и сколько курсов он слушает. Важно: анкета не должна размножить строки ученика, а отсутствие записей на курсы не должно выкинуть его из отчёта.

Верни столбцы:
- `full_name` — имя ученика;
- `plan` — тариф из анкеты;
- `courses_cnt` — число записей на курсы (целое; 0, если записей нет).
Сортировка: courses_cnt по убыванию, затем full_name по возрастанию. Ученики без записей на курсы обязаны присутствовать в результате со значением 0.

**Таблицы:**

- **students**: `student_id` integer 🔑 — ID ученика; `full_name` text — Имя ученика
- **student_profiles**: `student_id` integer 🔑 — ID ученика (ровно одна анкета на ученика); `city` text — Город; `plan` text — Тариф: free или premium
- **enrollments**: `enrollment_id` integer 🔑 — ID записи; `student_id` integer — ID ученика; `course_title` text — Название курса

**Колонки ответа:** `full_name`, `plan`, `courses_cnt`

**Пример ответа (первые строки):**

| full_name | plan | courses_cnt |
|---|---|---|
| Chloe Davis | premium | 3 |
| Alice Brown | premium | 2 |
| Emma Fisher | free | 2 |
| Henry Irwin | premium | 2 |
| Jack Kelly | premium | 2 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/jcr-academy-relations?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 41. Размножение строк после JOIN

*лёгкая* · Диалекты: PostgreSQL

Ты — младший аналитик стримингового сервиса PlayReel. Каталог хранится в shows (одна строка на сериал), а сезоны — в seasons: у сериала их может быть несколько. Коллега пожаловался, что после соединения этих таблиц сериалы «задвоились» и витрина каталога выглядит раздутой. Тебя просят показать масштаб бедствия: для каждого сериала, который после соединения занимает больше одной строки, вывести, во сколько строк он размножается.

Верни столбцы:
- `title` — название сериала;
- `join_rows` — сколько строк даёт этот сериал после соединения с сезонами (целое, строго больше 1).
Сортировка: join_rows по убыванию, затем title по возрастанию. Сериалы, дающие ровно одну строку или не имеющие сезонов, в результат не включай.

**Таблицы:**

- **shows**: `show_id` integer 🔑 — ID сериала; `title` text — Название сериала
- **seasons**: `season_id` integer 🔑 — ID сезона; `show_id` integer — ID сериала; `season_no` integer — Номер сезона

**Колонки ответа:** `title`, `join_rows`

**Пример ответа (первые строки):**

| title | join_rows |
|---|---|
| Silver Steppe | 4 |
| Iron Harbor | 3 |
| Paper Storm | 3 |
| Quantum Alley | 2 |
| Sunken City | 2 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/jcr-stream-fanout?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 42. Пары сопоставимых квартир

*лёгкая* · Диалекты: PostgreSQL

Ты аналитик в агентстве недвижимости UrbanNest. Оценщики просят инструмент для поиска сопоставимых объявлений: две квартиры из одного района с одинаковым числом комнат — идеальная пара, чтобы сверить цену. У тебя есть таблица listings с активными объявлениями.

Для каждого района найди все пары объявлений с одинаковым числом комнат. Каждая пара должна попасть в ответ ровно один раз: первым в паре идёт объявление с меньшим id. Объявления с неизвестным числом комнат (NULL) в пары не попадают.

Верни столбцы:
- `district` — район;
- `rooms` — число комнат;
- `listing_a` — id объявления с меньшим id в паре;
- `listing_b` — id объявления с большим id в паре;
- `price_gap` — абсолютная разница цен в паре (число как есть, без округления).

Сортировка: district по алфавиту, затем listing_a по возрастанию, затем listing_b по возрастанию. Если в районе три подходящих объявления, в ответ входят все три их попарные комбинации.

**Таблицы:**

- **listings**: `id` int 🔑 — Идентификатор объявления; `district` text — Район города; `rooms` int — Число комнат (NULL, если неизвестно); `price` numeric(12,2) — Цена, у.е.

**Колонки ответа:** `district`, `rooms`, `listing_a`, `listing_b`, `price_gap`

**Пример ответа (первые строки):**

| district | rooms | listing_a | listing_b | price_gap |
|---|---|---|---|---|
| Docklands | 2 | 10 | 12 | 3000.00 |
| Hillside | 3 | 7 | 8 | 10000.00 |
| Old Town | 1 | 4 | 5 | 5000.00 |
| Riverside | 2 | 1 | 2 | 15000.00 |
| Riverside | 3 | 3 | 13 | 5000.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/lsa-district-listing-pairs?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 43. Сотрудники и их отделы

*лёгкая* · Диалекты: PostgreSQL, ClickHouse

HR-отдел готовит справочник сотрудников с указанием подразделений, в которых они работают. Выведите имя сотрудника, фамилию сотрудника и название его отдела. Отсортируйте результат по фамилии сотрудника в алфавитном порядке.

**Таблицы:**

- **departments**: `id` serial 🔑 — Идентификатор отдела; `name` varchar(100) — Название отдела
- **employees**: `id` serial 🔑 — Идентификатор сотрудника; `first_name` varchar(50) — Имя сотрудника; `last_name` varchar(50) — Фамилия сотрудника; `department_id` integer → departments.id — Идентификатор отдела

**Колонки ответа:** `first_name`, `last_name`, `department_name`

**Пример ответа (первые строки):**

| first_name | last_name | department_name |
|---|---|---|
| Anna | Clark | Sales |
| Igor | Fedorov | Sales |
| Elena | Foster | Marketing |
| Alex | Johnson | Engineering |
| Paul | Newman | Engineering |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1775637019643-eunn?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 44. Популярные автомобили с несколькими бронированиями

*лёгкая* · Диалекты: PostgreSQL, ClickHouse

Сервис аренды автомобилей анализирует, какие машины пользуются повторным спросом. Найдите автомобили, которые были забронированы более одного раза, и покажите количество бронирований для каждого из них. Отсортируйте результат по популярности.

**Таблицы:**

- **vehicles**: `vehicle_id` serial 🔑 — Идентификатор автомобиля; `model` varchar(100) — Модель автомобиля; `license_plate` varchar(20) — Государственный номер; `daily_rate` decimal(8,2) — Стоимость аренды в сутки
- **bookings**: `booking_id` serial 🔑 — Идентификатор бронирования; `vehicle_id` integer → vehicles.vehicle_id — Идентификатор автомобиля; `customer_name` varchar(100) — Имя клиента; `booking_date` date — Дата бронирования

**Колонки ответа:** `vehicle_id`, `model`, `license_plate`, `booking_count`

**Пример ответа (первые строки):**

| vehicle_id | model | license_plate | booking_count |
|---|---|---|---|
| 2 | Honda Accord | XY789EF | 3 |
| 1 | Toyota Camry | AB123CD | 3 |
| 3 | BMW 3 Series | KL456GH | 2 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1777261814660-zi32?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 45. Первые пять посылок в пути

*лёгкая* · Диалекты: PostgreSQL, ClickHouse

Логистическая команда отслеживает отправления, которые сейчас находятся в дороге. Найдите посылки со статусом `в пути`, отсортируйте их по дате отправления по возрастанию и оставьте первые 5 записей. Для каждой посылки выведите данные о получателе из связанной таблицы.

**Таблицы:**

- **shipments**: `shipment_id` serial 🔑 — Идентификатор отправления; `package_code` varchar(20) — Код посылки; `weight` decimal(5,2) — Вес посылки; `status` varchar(30) — Статус доставки; `ship_date` date — Дата отправки; `recipient_id` integer → recipients.recipient_id — Идентификатор получателя
- **recipients**: `recipient_id` serial 🔑 — Идентификатор получателя; `full_name` varchar(100) — ФИО получателя; `city` varchar(50) — Город получателя; `phone` varchar(15) — Телефон получателя

**Колонки ответа:** `shipment_id`, `package_code`, `weight`, `status`, `ship_date`, `full_name`, `city`, `phone`

**Пример ответа (первые строки):**

| shipment_id | package_code | weight | status | ship_date | full_name | city | phone |
|---|---|---|---|---|---|---|---|
| 4 | PKG-2024-004 | 0.90 | in_transit | 2024-01-09 | Dmitri Orlov | Novosibirsk | 89994445566 |
| 1 | PKG-2024-001 | 2.50 | in_transit | 2024-01-10 | Maria Volkova | Moscow | 89991234567 |
| 6 | PKG-2024-006 | 2.30 | in_transit | 2024-01-11 | Maria Volkova | Moscow | 89991234567 |
| 3 | PKG-2024-003 | 3.80 | in_transit | 2024-01-12 | Olga Smirnova | Yekaterinburg | 89991112233 |
| 7 | PKG-2024-007 | 1.50 | in_transit | 2024-01-13 | Ivan Sokolov | Saint Petersburg | 89998765432 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1778256950814-4sv2?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 46. Топ игроки с высокой средней оценкой

*средняя* · Диалекты: PostgreSQL

Аналитики хотят выделить стабильно сильных игроков, учитывая только результативные матчи. Среди матчей в таблице `match_results` рассматривайте лишь те, где `score` > `60`. По таким матчам для каждого игрока посчитайте количество сыгранных игр (`games_played`) и среднюю оценку (`avg_score`). Оставьте только игроков, у которых таких матчей (с `score` > `60`) не меньше `3` и средняя оценка по ним превышает `75`. Выведите имя игрока (`name`), количество таких матчей и их среднюю оценку, отсортировав результат по средней оценке `avg_score` в порядке убывания.

**Таблицы:**

- **players**: `player_id` int 🔑; `name` varchar(100); `country` varchar(50); `join_date` date
- **games**: `game_id` int 🔑; `title` varchar(100); `release_year` integer; `genre` varchar(50)
- **match_results**: `match_id` int 🔑; `player_id` integer → players.player_id; `game_id` integer → games.game_id; `score` integer; `match_date` date
- **achievements**: `achievement_id` int 🔑; `player_id` integer → players.player_id; `title` varchar(100); `unlocked_date` date

**Колонки ответа:** `name`, `games_played`, `avg_score`

**Пример ответа (первые строки):**

| name | games_played | avg_score |
|---|---|---|
| Carlos Martinez | 3 | 92.0000000000000000 |
| Elena Petrova | 4 | 83.0000000000000000 |
| Alice Johnson | 3 | 82.6666666666666667 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1779047665720-a2sr?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 47. Анализ прибыльности маршрутов авиакомпании

*средняя* · Диалекты: PostgreSQL

Авиакомпания хочет выявить самые прибыльные маршруты в своём портфеле. Найдите маршруты, на которых в среднем стоимость билета составляет более 250 долларов, сгруппировав данные по направлениям и указав количество разных рейсов, среднюю стоимость билета и общую выручку. Результаты отсортируйте по убыванию общей выручки и выведите столбцы: маршрут (направление от аэропорта отправления к аэропорту прибытия), количество разных рейсов, среднюю стоимость билета и общую выручку. Округлите `avg_ticket_price`, `total_revenue` до двух знаков после запятой.

**Таблицы:**

- **airports**: `airport_id` serial 🔑; `airport_code` varchar(3); `city_name` varchar(100)
- **flights**: `flight_id` serial 🔑; `origin_airport_id` integer → airports.airport_id; `destination_airport_id` integer → airports.airport_id; `flight_number` varchar(10)
- **bookings**: `booking_id` serial 🔑; `flight_id` integer → flights.flight_id; `ticket_price` decimal(10,2)
- **passengers**: `passenger_id` serial 🔑; `booking_id` integer → bookings.booking_id; `passenger_name` varchar(100)

**Колонки ответа:** `route`, `flights_count`, `avg_ticket_price`, `total_revenue`

**Пример ответа (первые строки):**

| route | flights_count | avg_ticket_price | total_revenue |
|---|---|---|---|
| JFK-LAX | 3 | 285.00 | 1710.00 |
| JFK-LHR | 2 | 450.00 | 1350.00 |
| LAX-JFK | 2 | 290.00 | 1160.00 |
| LHR-CDG | 1 | 380.00 | 380.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1782644485879-37vn?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 48. Товары с высоким оборотом и рентабельностью

*средняя* · Диалекты: PostgreSQL

Менеджер склада анализирует эффективность товаров. Нужно найти товары, которые продали более 50 единиц, при этом средняя цена продажи каждого товара должна быть не менее чем на 20% выше его себестоимости. Результат должен содержать название товара, количество проданных единиц, среднюю цену продажи и себестоимость, отсортированный по убыванию количества продаж.

**Таблицы:**

- **products**: `product_id` serial 🔑; `product_name` varchar(100); `cost_price` decimal(10,2)
- **warehouses**: `warehouse_id` serial 🔑; `warehouse_name` varchar(100); `location` varchar(100)
- **stock**: `stock_id` serial 🔑; `product_id` integer → products.product_id; `warehouse_id` integer → warehouses.warehouse_id; `quantity_on_hand` integer
- **sales**: `sale_id` serial 🔑; `product_id` integer → products.product_id; `warehouse_id` integer → warehouses.warehouse_id; `quantity_sold` integer; `selling_price` decimal(10,2)

**Колонки ответа:** `product_name`, `total_units_sold`, `avg_selling_price`, `cost_price`

**Пример ответа (первые строки):**

| product_name | total_units_sold | avg_selling_price | cost_price |
|---|---|---|---|
| Mechanical Keyboard | 60 | 96.5000000000000000 | 65.00 |
| HDMI Cable | 60 | 4.5000000000000000 | 3.00 |
| Wireless Mouse | 55 | 22.0000000000000000 | 15.00 |
| Laptop Dell XPS | 55 | 665.0000000000000000 | 450.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1787750925236-chyg?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 49. Самые активные авторы по количеству опубликованных статей

*средняя* · Диалекты: PostgreSQL

В портале новостей требуется выявить авторов, которые опубликовали более 3 статей за всё время, и показать их имена, общее количество разных публикаций и среднее количество комментариев на одну статью (статьи без комментариев тоже учитываются). Результаты отсортировать по убыванию количества статей, затем по убыванию среднего числа комментариев. Округлите `avg_comments_per_article` до двух знаков после запятой.

**Таблицы:**

- **authors**: `author_id` serial 🔑; `author_name` varchar(100); `email` varchar(100)
- **articles**: `article_id` serial 🔑; `author_id` integer → authors.author_id; `title` varchar(255); `published_date` date
- **comments**: `comment_id` serial 🔑; `article_id` integer → articles.article_id; `commenter_name` varchar(100); `comment_text` text; `created_at` timestamp
- **categories**: `category_id` serial 🔑; `article_id` integer → articles.article_id; `category_name` varchar(50)

**Колонки ответа:** `author_name`, `total_articles`, `avg_comments_per_article`

**Пример ответа (первые строки):**

| author_name | total_articles | avg_comments_per_article |
|---|---|---|
| Elena Petrova | 4 | 2.75 |
| Ivan Sokolov | 4 | 1.75 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1787751852906-h5a1?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 50. Загруженные отделения клиники

*средняя* · Диалекты: PostgreSQL

Администрация многопрофильной клиники хочет понять, какие отделения реально перегружены приёмами пациентов, чтобы перераспределить врачей.

**Таблицы:**

- **departments**: `department_id` serial 🔑; `name` varchar(100)
- **doctors**: `doctor_id` serial 🔑; `full_name` varchar(100); `department_id` integer → departments.department_id
- **patients**: `patient_id` serial 🔑; `full_name` varchar(100)
- **visits**: `visit_id` serial 🔑; `patient_id` integer → patients.patient_id; `doctor_id` integer → doctors.doctor_id; `visit_date` date; `cost` decimal(10,2)

**Колонки ответа:** `department_name`, `visit_count`, `avg_cost`

**Пример ответа (первые строки):**

| department_name | visit_count | avg_cost |
|---|---|---|
| Kardiologiya | 5 | 1620.00 |
| Pediatriya | 3 | 750.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1791184175847-gz7f?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 51. Лучшие гостиничные номера по среднему рейтингу и доходу

*средняя* · Диалекты: PostgreSQL

Сеть отелей анализирует качество своих номеров на основе отзывов гостей и финансовых показателей. Для каждого номера нужно рассчитать средний рейтинг из всех отзывов и общий доход от бронирований, но только для номеров, которые получили как минимум 3 отзыва и сгенерировали доход не менее 5000 рублей.

Вывести номер комнаты, тип номера, средний рейтинг (округлить до 2 знаков), общий доход и количество отзывов. Отсортировать по среднему рейтингу от большего к меньшему, при равенстве рейтинга — по доходу от большего к меньшему.

**Таблицы:**

- **hotels**: `hotel_id` serial 🔑; `hotel_name` varchar(100)
- **rooms**: `room_id` serial 🔑; `hotel_id` integer → hotels.hotel_id; `room_number` varchar(20); `room_type` varchar(50)
- **reservations**: `reservation_id` serial 🔑; `room_id` integer → rooms.room_id; `guest_name` varchar(100); `total_price` decimal(10,2)
- **reviews**: `review_id` serial 🔑; `reservation_id` integer → reservations.reservation_id; `rating` integer; `comment` text

**Колонки ответа:** `room_number`, `room_type`, `avg_rating`, `total_revenue`, `review_count`

**Пример ответа (первые строки):**

| room_number | room_type | avg_rating | total_revenue | review_count |
|---|---|---|---|---|
| 305 | Suite | 4.75 | 13000.00 | 4 |
| 201 | Deluxe | 4.67 | 7500.00 | 3 |
| 101 | Standard | 4.33 | 6500.00 | 3 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1789653316245-yp2u?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 52. Топ компании по среднему рейтингу отзывов соискателей

*средняя* · Диалекты: PostgreSQL

На портале размещены вакансии от разных компаний, и каждый соискатель может оставить отзыв о своем опыте собеседования. Найдите компании, у которых средний рейтинг всех отзывов составляет не менее 4.0 балла, отсортируйте их по среднему рейтингу в убывающем порядке и выведите название компании, количество полученных отзывов и средний рейтинг (округленный до одного знака после запятой).

**Таблицы:**

- **companies**: `id` serial 🔑; `name` varchar(100); `industry` varchar(50)
- **job_postings**: `id` serial 🔑; `company_id` integer → companies.id; `title` varchar(150); `salary_min` decimal(10,2); `salary_max` decimal(10,2)
- **applicants**: `id` serial 🔑; `name` varchar(100); `email` varchar(100)
- **reviews**: `id` serial 🔑; `job_posting_id` integer → job_postings.id; `applicant_id` integer → applicants.id; `rating` integer; `review_text` text

**Колонки ответа:** `name`, `review_count`, `avg_rating`

**Пример ответа (первые строки):**

| name | review_count | avg_rating |
|---|---|---|
| GreenEnergy Inc | 2 | 5.0 |
| CloudSync Systems | 2 | 4.5 |
| TechCore Solutions | 5 | 4.0 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1785332014250-r4f3?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 53. Прибыльные номера отеля за квартал

*средняя* · Диалекты: PostgreSQL

Сеть отелей проводит анализ доходности своего парка номеров. Нужно найти все категории номеров, которые принесли в этом квартале выручку выше среднего по всем категориям. Для каждой такой категории вывести название, количество бронирований, среднюю цену за ночь и общую выручку за период. Результат отсортировать по выручке — от наибольшей к наименьшей.

**Таблицы:**

- **room_categories**: `category_id` serial 🔑; `category_name` varchar(100)
- **rooms**: `room_id` serial 🔑; `room_number` varchar(20); `category_id` integer → room_categories.category_id
- **reservations**: `reservation_id` serial 🔑; `room_id` integer → rooms.room_id; `check_in` date; `check_out` date; `nightly_rate` decimal(10, 2)
- **reservation_dates**: `reservation_id` integer 🔑; `revenue` decimal(12, 2)

**Колонки ответа:** `category_name`, `booking_count`, `avg_nightly_rate`, `total_revenue`

**Пример ответа (первые строки):**

| category_name | booking_count | avg_nightly_rate | total_revenue |
|---|---|---|---|
| Deluxe | 4 | 180.00 | 4680.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1789563056453-x45d?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 54. Врачи с максимальной нагрузкой пациентов

*средняя* · Диалекты: PostgreSQL

В больнице нужно выявить врачей, которые имеют дело с наиболее сложными случаями. Найдите всех врачей, у которых средний возраст пациентов превышает 50 лет, и выведите врача, количество разных пациентов и средний возраст. Результаты отсортируйте по среднему возрасту в порядке убывания, затем по имени врача в алфавитном порядке. Округлите `average_patient_age` до одного знака после запятой.

**Таблицы:**

- **doctors**: `doctor_id` serial 🔑; `name` varchar(100); `specialty` varchar(50)
- **patients**: `patient_id` serial 🔑; `name` varchar(100); `age` integer; `admission_date` date
- **appointments**: `appointment_id` serial 🔑; `doctor_id` integer → doctors.doctor_id; `patient_id` integer → patients.patient_id; `visit_date` date; `notes` text
- **diagnoses**: `diagnosis_id` serial 🔑; `appointment_id` integer → appointments.appointment_id; `condition` varchar(100); `severity` varchar(20)

**Колонки ответа:** `doctor_name`, `patient_count`, `average_patient_age`

**Пример ответа (первые строки):**

| doctor_name | patient_count | average_patient_age |
|---|---|---|
| Ivan Petrov | 3 | 65.0 |
| Alexei Romanov | 2 | 56.5 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1787905556716-aupk?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 55. Анализ убыточности страховых полисов по регионам

*средняя* · Диалекты: PostgreSQL

Компания анализирует рентабельность своего портфеля полисов по географическим регионам. Необходимо найти все регионы, в которых выплаты по претензиям превышают полученные премии в сумме более чем на 50 000 рублей, что свидетельствует об убыточности.

Для каждого найденного региона вывести его название, общую сумму полученных премий, общую сумму выплаченных претензий и размер убытка (разница между выплатами и премиями). Результаты отсортировать по размеру убытка в порядке убывания.

**Таблицы:**

- **regions**: `region_id` serial 🔑; `region_name` varchar(100)
- **policies**: `policy_id` serial 🔑; `region_id` integer → regions.region_id; `policy_number` varchar(50); `premium_amount` decimal(10,2); `issue_date` date
- **claims**: `claim_id` serial 🔑; `policy_id` integer → policies.policy_id; `claim_number` varchar(50); `claim_amount` decimal(10,2); `claim_date` date; `status` varchar(20)
- **claim_payments**: `payment_id` serial 🔑; `claim_id` integer → claims.claim_id; `payment_amount` decimal(10,2); `payment_date` date

**Колонки ответа:** `region_name`, `total_premiums`, `total_payments`, `loss_amount`

**Пример ответа (первые строки):**

| region_name | total_premiums | total_payments | loss_amount |
|---|---|---|---|
| Moskva | 235000.00 | 365000.00 | 130000.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1790319194211-v0bh?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 56. Урожайность фермеров-лидеров по культурам

*средняя* · Диалекты: PostgreSQL

На сельскохозяйственной бирже нужно определить фермеров, которые выращивают несколько культур и собирают в среднем не менее 500 центнеров урожая на одну культуру. Найти идентификатор фермера, его имя, количество разных выращиваемых культур и среднюю урожайность, отсортировав по средней урожайности в порядке убывания. Округлите `avg_yield` до двух знаков после запятой.

**Таблицы:**

- **farmers**: `farmer_id` serial 🔑; `name` varchar(100); `region` varchar(50)
- **crops**: `crop_id` serial 🔑; `crop_name` varchar(100); `crop_type` varchar(50)
- **harvest_records**: `record_id` serial 🔑; `farmer_id` integer → farmers.farmer_id; `crop_id` integer → crops.crop_id; `harvest_year` integer; `yield_centners` decimal(10, 2)
- **soil_quality**: `quality_id` serial 🔑; `farmer_id` integer → farmers.farmer_id; `soil_type` varchar(50); `ph_level` decimal(3, 1)

**Колонки ответа:** `farmer_id`, `name`, `crops_count`, `avg_yield`

**Пример ответа (первые строки):**

| farmer_id | name | crops_count | avg_yield |
|---|---|---|---|
| 5 | Mikhail Smirnov | 3 | 560.00 |
| 2 | Elena Volkova | 2 | 555.00 |
| 3 | Sergei Orlov | 2 | 505.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/ai-1787822297972-f1yr?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**
