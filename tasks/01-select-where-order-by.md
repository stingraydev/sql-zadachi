# SELECT, WHERE, ORDER BY — выборка и фильтрация

[← Ко всем темам](../README.md)

## 1. Лекарства, которые продаются без рецепта

*лёгкая* · Диалекты: PostgreSQL, MySQL, ClickHouse

На дежурстве в аптеке часто спрашивают, какие лекарства можно купить сразу, без рецепта врача. Выведите название и цену лекарств, у которых `requires_prescription = false`. Отсортируйте результат по названию.

**Таблицы:**

- **Customer**: `id` int 🔑 — Идентификатор клиента; `full_name` varchar(100) — ФИО клиента; `birth_date` date — Дата рождения; `phone` varchar(30) — Телефон клиента; `city` varchar(100) — Город клиента
- **Pharmacist**: `id` int 🔑 — Идентификатор фармацевта; `last_name` varchar(100) — Фамилия фармацевта; `hire_date` date — Дата приёма на работу; `specialty` varchar(50) — Специализация фармацевта
- **Medication**: `id` int 🔑 — Идентификатор лекарства; `name` varchar(100) — Название лекарства; `manufacturer` varchar(100) — Производитель; `category` varchar(50) — Категория лекарства; `price` decimal(10,2) — Цена лекарства; `requires_prescription` boolean — Признак рецептурного отпуска
- **Purchase**: `id` int 🔑 — Идентификатор покупки; `customer_id` int → Customer.id — Идентификатор клиента; `pharmacist_id` int → Pharmacist.id — Идентификатор фармацевта; `purchase_date` date — Дата покупки; `payment_method` varchar(20) — Способ оплаты
- **PurchaseItem**: `id` int 🔑 — Идентификатор позиции покупки; `purchase_id` int → Purchase.id — Идентификатор покупки; `medication_id` int → Medication.id — Идентификатор лекарства; `quantity` int — Количество; `unit_price` decimal(10,2) — Цена за единицу

**Колонки ответа:** `name`, `price`

**Пример ответа (первые строки):**

| name | price |
|---|---|
| Aspirin | 4.50 |
| Ibuprofen | 5.80 |
| VitaminC | 6.20 |
| VitaminD3 | 9.50 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/pharma-1?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 2. Количество клиентов из Берлина

*лёгкая* · Диалекты: PostgreSQL, MySQL, ClickHouse

Маркетинг аптеки готовит локальную акцию для жителей Берлина и хочет оценить размер клиентской базы в этом городе. Посчитайте, сколько клиентов аптеки указали город `Berlin`.

**Таблицы:**

- **Customer**: `id` int 🔑 — Идентификатор клиента; `full_name` varchar(100) — ФИО клиента; `birth_date` date — Дата рождения; `phone` varchar(30) — Телефон клиента; `city` varchar(100) — Город клиента
- **Pharmacist**: `id` int 🔑 — Идентификатор фармацевта; `last_name` varchar(100) — Фамилия фармацевта; `hire_date` date — Дата приёма на работу; `specialty` varchar(50) — Специализация фармацевта
- **Medication**: `id` int 🔑 — Идентификатор лекарства; `name` varchar(100) — Название лекарства; `manufacturer` varchar(100) — Производитель; `category` varchar(50) — Категория лекарства; `price` decimal(10,2) — Цена лекарства; `requires_prescription` boolean — Признак рецептурного отпуска
- **Purchase**: `id` int 🔑 — Идентификатор покупки; `customer_id` int → Customer.id — Идентификатор клиента; `pharmacist_id` int → Pharmacist.id — Идентификатор фармацевта; `purchase_date` date — Дата покупки; `payment_method` varchar(20) — Способ оплаты
- **PurchaseItem**: `id` int 🔑 — Идентификатор позиции покупки; `purchase_id` int → Purchase.id — Идентификатор покупки; `medication_id` int → Medication.id — Идентификатор лекарства; `quantity` int — Количество; `unit_price` decimal(10,2) — Цена за единицу

**Колонки ответа:** `count`

**Пример ответа (первые строки):**

| count |
|---|
| 2 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/pharma-2?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 3. Платиновые участники программы лояльности

*лёгкая* · Диалекты: PostgreSQL, MySQL, ClickHouse

VIP-менеджер авиакомпании готовит индивидуальные апгрейды для самых ценных участников программы лояльности. Выведите имя и страну каждого участника со статусом `platinum`. Отсортируйте результат по имени участника.

**Таблицы:**

- **Member**: `id` int 🔑 — Идентификатор участника; `full_name` varchar(100) — Полное имя участника; `status_tier` varchar(20) — Уровень статуса; `joined_at` date — Дата вступления; `country` varchar(100) — Страна участника
- **Flight**: `id` int 🔑 — Идентификатор рейса; `route` varchar(50) — Маршрут рейса; `distance_miles` int — Расстояние в милях; `base_class` varchar(20) — Класс обслуживания; `flight_date` date — Дата рейса
- **MileEarning**: `id` int 🔑 — Идентификатор начисления; `member_id` int → Member.id — Идентификатор участника; `flight_id` int → Flight.id — Идентификатор рейса; `miles_earned` int — Начислено миль; `earned_date` date — Дата начисления
- **Redemption**: `id` int 🔑 — Идентификатор обмена; `member_id` int → Member.id — Идентификатор участника; `redeemed_date` date — Дата обмена; `miles_spent` int — Потрачено миль; `item_redeemed` varchar(100) — Полученная награда

**Колонки ответа:** `full_name`, `country`

**Пример ответа (первые строки):**

| full_name | country |
|---|---|
| Olivia Bennett | USA |
| Sophia Laurent | France |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/loyal-1?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 4. Количество дальних рейсов

*лёгкая* · Диалекты: PostgreSQL, MySQL, ClickHouse

Пиар-отдел авиакомпании готовит баннер о масштабе маршрутной сети и хочет указать число действительно дальних направлений. Посчитайте, сколько рейсов в каталоге имеют дальность более 5000 миль.

**Таблицы:**

- **Member**: `id` int 🔑 — Идентификатор участника; `full_name` varchar(100) — Полное имя участника; `status_tier` varchar(20) — Уровень статуса; `joined_at` date — Дата вступления; `country` varchar(100) — Страна участника
- **Flight**: `id` int 🔑 — Идентификатор рейса; `route` varchar(50) — Маршрут рейса; `distance_miles` int — Расстояние в милях; `base_class` varchar(20) — Класс обслуживания; `flight_date` date — Дата рейса
- **MileEarning**: `id` int 🔑 — Идентификатор начисления; `member_id` int → Member.id — Идентификатор участника; `flight_id` int → Flight.id — Идентификатор рейса; `miles_earned` int — Начислено миль; `earned_date` date — Дата начисления
- **Redemption**: `id` int 🔑 — Идентификатор обмена; `member_id` int → Member.id — Идентификатор участника; `redeemed_date` date — Дата обмена; `miles_spent` int — Потрачено миль; `item_redeemed` varchar(100) — Полученная награда

**Колонки ответа:** `count`

**Пример ответа (первые строки):**

| count |
|---|
| 4 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/loyal-2?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 5. Фитнес-клубы в Берлине

*лёгкая* · Диалекты: PostgreSQL, MySQL, ClickHouse

Региональный директор готовит выездной аудит берлинских филиалов сети и хочет получить полный список клубов в городе. Выведите названия клубов, расположенных в Берлине. Отсортируйте результат по названию клуба.

**Таблицы:**

- **Club**: `id` int 🔑 — Идентификатор клуба; `club_name` varchar(100) — Название клуба; `city` varchar(100) — Город клуба; `opened_at` date — Дата открытия
- **Trainer**: `id` int 🔑 — Идентификатор тренера; `full_name` varchar(100) — Имя тренера; `club_id` int → Club.id — Идентификатор клуба; `hire_date` date — Дата приёма на работу; `specialization` varchar(50) — Специализация тренера
- **MemberAccount**: `id` int 🔑 — Идентификатор клиента; `full_name` varchar(100) — Имя клиента; `signup_date` date — Дата регистрации; `monthly_fee` decimal(10,2) — Ежемесячная плата; `plan_type` varchar(20) — Тип абонемента; `home_club_id` int → Club.id — Идентификатор клуба
- **ClassSession**: `id` int 🔑 — Идентификатор занятия; `class_name` varchar(100) — Название занятия; `club_id` int → Club.id — Идентификатор клуба; `trainer_id` int → Trainer.id — Идентификатор тренера; `session_date` date — Дата занятия; `capacity` int — Вместимость занятия
- **Booking**: `id` int 🔑 — Идентификатор записи; `member_id` int → MemberAccount.id — Идентификатор клиента; `session_id` int → ClassSession.id — Идентификатор занятия; `attended` boolean — Признак посещения; `booked_at` date — Дата записи

**Колонки ответа:** `club_name`

**Пример ответа (первые строки):**

| club_name |
|---|
| PowerHouse Charlottenburg |
| PowerHouse Kreuzberg |
| PowerHouse Mitte |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/fit-1?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 6. Количество Premium-клиентов

*лёгкая* · Диалекты: PostgreSQL, MySQL, ClickHouse

Команда продукта оценивает результат прошлогоднего апсейл-флоу и хочет узнать, сколько клиентов сейчас пользуются тарифом `Premium`. Посчитайте количество таких клиентов.

**Таблицы:**

- **Club**: `id` int 🔑 — Идентификатор клуба; `club_name` varchar(100) — Название клуба; `city` varchar(100) — Город клуба; `opened_at` date — Дата открытия
- **Trainer**: `id` int 🔑 — Идентификатор тренера; `full_name` varchar(100) — Имя тренера; `club_id` int → Club.id — Идентификатор клуба; `hire_date` date — Дата приёма на работу; `specialization` varchar(50) — Специализация тренера
- **MemberAccount**: `id` int 🔑 — Идентификатор клиента; `full_name` varchar(100) — Имя клиента; `signup_date` date — Дата регистрации; `monthly_fee` decimal(10,2) — Ежемесячная плата; `plan_type` varchar(20) — Тип абонемента; `home_club_id` int → Club.id — Идентификатор клуба
- **ClassSession**: `id` int 🔑 — Идентификатор занятия; `class_name` varchar(100) — Название занятия; `club_id` int → Club.id — Идентификатор клуба; `trainer_id` int → Trainer.id — Идентификатор тренера; `session_date` date — Дата занятия; `capacity` int — Вместимость занятия
- **Booking**: `id` int 🔑 — Идентификатор записи; `member_id` int → MemberAccount.id — Идентификатор клиента; `session_id` int → ClassSession.id — Идентификатор занятия; `attended` boolean — Признак посещения; `booked_at` date — Дата записи

**Колонки ответа:** `count`

**Пример ответа (первые строки):**

| count |
|---|
| 4 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/fit-2?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 7. Пятизвёздочные отели сети

*лёгкая* · Диалекты: PostgreSQL, MySQL, ClickHouse

Премиальный консьерж готовит подборку для VIP-клиента, которому нужны только отели высшей категории. Выведите название и город всех отелей сети со звёздностью `5`. Отсортируйте результат по названию отеля.

**Таблицы:**

- **Hotel**: `id` int 🔑 — Идентификатор отеля; `hotel_name` varchar(100) — Название отеля; `city` varchar(100) — Город отеля; `star_rating` int — Звёздность отеля; `opened_year` int — Год открытия
- **Room**: `id` int 🔑 — Идентификатор номера; `hotel_id` int → Hotel.id — Идентификатор отеля; `room_type` varchar(50) — Тип номера; `floor` int — Этаж; `max_occupancy` int — Максимальная вместимость; `base_price` decimal(10,2) — Базовая цена
- **Guest**: `id` int 🔑 — Идентификатор гостя; `full_name` varchar(100) — Имя гостя; `country` varchar(100) — Страна гостя; `registered_at` date — Дата регистрации
- **Reservation**: `id` int 🔑 — Идентификатор бронирования; `guest_id` int → Guest.id — Идентификатор гостя; `room_id` int → Room.id — Идентификатор номера; `check_in` date — Дата заезда; `check_out` date — Дата выезда; `total_paid` decimal(10,2) — Итоговая сумма; `status` varchar(20) — Статус бронирования
- **ServiceCharge**: `id` int 🔑 — Идентификатор начисления; `reservation_id` int → Reservation.id — Идентификатор бронирования; `service_type` varchar(50) — Тип услуги; `charge_amount` decimal(10,2) — Сумма начисления; `charged_at` date — Дата начисления

**Колонки ответа:** `hotel_name`, `city`

**Пример ответа (первые строки):**

| hotel_name | city |
|---|---|
| Grand Plaza | Paris |
| Royal Garden | London |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/hotel-1?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 8. Рок-артисты фестивальной базы

*лёгкая* · Диалекты: PostgreSQL, MySQL, ClickHouse

Букер планирует серию рок-фестивалей и составляет шорт-лист исполнителей, которые подходят под жанровую концепцию. Выведите имя и страну каждого артиста жанра `Rock`. Отсортируйте результат по имени артиста.

**Таблицы:**

- **Festival**: `id` int 🔑 — Идентификатор фестиваля; `festival_name` varchar(100) — Название фестиваля; `year` int — Год проведения; `location` varchar(100) — Место проведения; `attendance` int — Число посетителей
- **Stage**: `id` int 🔑 — Идентификатор сцены; `festival_id` int → Festival.id — Идентификатор фестиваля; `stage_name` varchar(100) — Название сцены; `capacity` int — Вместимость сцены
- **Artist**: `id` int 🔑 — Идентификатор артиста; `artist_name` varchar(100) — Имя артиста; `genre` varchar(50) — Музыкальный жанр; `country` varchar(100) — Страна артиста
- **Performance**: `id` int 🔑 — Идентификатор выступления; `festival_id` int → Festival.id — Идентификатор фестиваля; `stage_id` int → Stage.id — Идентификатор сцены; `artist_id` int → Artist.id — Идентификатор артиста; `start_time` timestamp — Дата и время начала; `duration_min` int — Длительность в минутах; `fee_paid` decimal(12,2) — Выплаченный гонорар
- **Sponsor**: `id` int 🔑 — Идентификатор спонсора; `sponsor_name` varchar(100) — Название спонсора; `sponsorship_amount` decimal(12,2) — Сумма спонсорства; `festival_id` int → Festival.id — Идентификатор фестиваля; `tier` varchar(20) — Уровень спонсорства

**Колонки ответа:** `artist_name`, `country`

**Пример ответа (первые строки):**

| artist_name | country |
|---|---|
| Iron Sparrow | UK |
| River Stones | Ireland |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/fest-1?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 9. Количество просторных номеров

*лёгкая* · Диалекты: PostgreSQL, MySQL, ClickHouse

Тур-оператор бронирует серию семейных туров и хочет понять, сколько в сети номеров подходит для размещения больше двух человек. Посчитайте количество номеров, у которых `max_occupancy > 2`.

**Таблицы:**

- **Hotel**: `id` int 🔑 — Идентификатор отеля; `hotel_name` varchar(100) — Название отеля; `city` varchar(100) — Город отеля; `star_rating` int — Звёздность отеля; `opened_year` int — Год открытия
- **Room**: `id` int 🔑 — Идентификатор номера; `hotel_id` int → Hotel.id — Идентификатор отеля; `room_type` varchar(50) — Тип номера; `floor` int — Этаж; `max_occupancy` int — Максимальная вместимость; `base_price` decimal(10,2) — Базовая цена
- **Guest**: `id` int 🔑 — Идентификатор гостя; `full_name` varchar(100) — Имя гостя; `country` varchar(100) — Страна гостя; `registered_at` date — Дата регистрации
- **Reservation**: `id` int 🔑 — Идентификатор бронирования; `guest_id` int → Guest.id — Идентификатор гостя; `room_id` int → Room.id — Идентификатор номера; `check_in` date — Дата заезда; `check_out` date — Дата выезда; `total_paid` decimal(10,2) — Итоговая сумма; `status` varchar(20) — Статус бронирования
- **ServiceCharge**: `id` int 🔑 — Идентификатор начисления; `reservation_id` int → Reservation.id — Идентификатор бронирования; `service_type` varchar(50) — Тип услуги; `charge_amount` decimal(10,2) — Сумма начисления; `charged_at` date — Дата начисления

**Колонки ответа:** `count`

**Пример ответа (первые строки):**

| count |
|---|
| 6 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/hotel-2?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 10. Количество фестивалей в 2024 году

*лёгкая* · Диалекты: PostgreSQL, MySQL, ClickHouse

Команда годового отчёта подводит итоги 2024 года и хочет быстро оценить масштаб фестивальной программы. Посчитайте, сколько фестивалей в базе имеют год `2024`.

**Таблицы:**

- **Festival**: `id` int 🔑 — Идентификатор фестиваля; `festival_name` varchar(100) — Название фестиваля; `year` int — Год проведения; `location` varchar(100) — Место проведения; `attendance` int — Число посетителей
- **Stage**: `id` int 🔑 — Идентификатор сцены; `festival_id` int → Festival.id — Идентификатор фестиваля; `stage_name` varchar(100) — Название сцены; `capacity` int — Вместимость сцены
- **Artist**: `id` int 🔑 — Идентификатор артиста; `artist_name` varchar(100) — Имя артиста; `genre` varchar(50) — Музыкальный жанр; `country` varchar(100) — Страна артиста
- **Performance**: `id` int 🔑 — Идентификатор выступления; `festival_id` int → Festival.id — Идентификатор фестиваля; `stage_id` int → Stage.id — Идентификатор сцены; `artist_id` int → Artist.id — Идентификатор артиста; `start_time` timestamp — Дата и время начала; `duration_min` int — Длительность в минутах; `fee_paid` decimal(12,2) — Выплаченный гонорар
- **Sponsor**: `id` int 🔑 — Идентификатор спонсора; `sponsor_name` varchar(100) — Название спонсора; `sponsorship_amount` decimal(12,2) — Сумма спонсорства; `festival_id` int → Festival.id — Идентификатор фестиваля; `tier` varchar(20) — Уровень спонсорства

**Колонки ответа:** `count`

**Пример ответа (первые строки):**

| count |
|---|
| 3 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/fest-2?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 11. Виды животных на грани исчезновения

*лёгкая* · Диалекты: PostgreSQL, MySQL, ClickHouse

Куратор по сохранению видов готовит просветительский баннер о редких животных в зоопарке. Выведите названия видов, у которых статус сохранения равен `endangered` или `critically_endangered`, а также сам статус. Отсортируйте результат по названию вида.

**Таблицы:**

- **Section**: `id` int 🔑 — Идентификатор секции; `section_name` varchar(100) — Название секции; `climate_zone` varchar(50) — Климатическая зона; `area_sqm` int — Площадь в кв. метрах
- **Species**: `id` int 🔑 — Идентификатор вида; `species_name` varchar(100) — Название вида; `conservation_status` varchar(50) — Охранный статус; `native_continent` varchar(50) — Родной континент
- **Animal**: `id` int 🔑 — Идентификатор животного; `name` varchar(100) — Кличка животного; `species_id` int → Species.id — Идентификатор вида; `section_id` int → Section.id — Идентификатор секции; `birth_date` date — Дата рождения; `gender` varchar(1) — Пол животного
- **Caretaker**: `id` int 🔑 — Идентификатор смотрителя; `full_name` varchar(100) — Имя смотрителя; `hire_date` date — Дата приёма на работу; `role` varchar(50) — Должность смотрителя
- **FeedingLog**: `id` int 🔑 — Идентификатор записи; `animal_id` int → Animal.id — Идентификатор животного; `caretaker_id` int → Caretaker.id — Идентификатор смотрителя; `feed_date` date — Дата кормления; `food_type` varchar(50) — Тип корма; `amount_kg` decimal(8,2) — Объём корма в кг

**Колонки ответа:** `species_name`, `conservation_status`

**Пример ответа (первые строки):**

| species_name | conservation_status |
|---|---|
| African Elephant | endangered |
| Black Rhino | critically_endangered |
| Sumatran Orangutan | critically_endangered |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/zoo-1?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 12. Количество животных в секции Africa Savanna

*лёгкая* · Диалекты: PostgreSQL, MySQL, ClickHouse

Старший зоотехник готовит план рассадки в новой секции и сначала хочет понять текущую загруженность саванны. Посчитайте, сколько животных сейчас живёт в секции `Africa Savanna`.

**Таблицы:**

- **Section**: `id` int 🔑 — Идентификатор секции; `section_name` varchar(100) — Название секции; `climate_zone` varchar(50) — Климатическая зона; `area_sqm` int — Площадь в кв. метрах
- **Species**: `id` int 🔑 — Идентификатор вида; `species_name` varchar(100) — Название вида; `conservation_status` varchar(50) — Охранный статус; `native_continent` varchar(50) — Родной континент
- **Animal**: `id` int 🔑 — Идентификатор животного; `name` varchar(100) — Кличка животного; `species_id` int → Species.id — Идентификатор вида; `section_id` int → Section.id — Идентификатор секции; `birth_date` date — Дата рождения; `gender` varchar(1) — Пол животного
- **Caretaker**: `id` int 🔑 — Идентификатор смотрителя; `full_name` varchar(100) — Имя смотрителя; `hire_date` date — Дата приёма на работу; `role` varchar(50) — Должность смотрителя
- **FeedingLog**: `id` int 🔑 — Идентификатор записи; `animal_id` int → Animal.id — Идентификатор животного; `caretaker_id` int → Caretaker.id — Идентификатор смотрителя; `feed_date` date — Дата кормления; `food_type` varchar(50) — Тип корма; `amount_kg` decimal(8,2) — Объём корма в кг

**Колонки ответа:** `count`

**Пример ответа (первые строки):**

| count |
|---|
| 5 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/zoo-2?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 13. Витрина товаров: переименуй колонки

*лёгкая* · Диалекты: PostgreSQL

В каталоге «Котомаркета» есть таблица `products` с товарами для котов: `id`, `title` (название), `price` (цена), `stock` (остаток на складе).

Витрине нужны человеко-понятные заголовки колонок. Напиши запрос, который выбирает из `products` **три** столбца и даёт им явные псевдонимы через `AS`:

- `title` → `naimenovanie`
- `price` → `cena`
- `stock` → `ostatok`

Выведи **все** строки таблицы. Столбец `id` в результат не включай.

Порядок строк не важен. Порядок столбцов должен быть именно таким: `naimenovanie`, `cena`, `ostatok`.

**Таблицы:**

- **products**: `id` integer 🔑 — Идентификатор товара (первичный ключ); `title` text — Название товара; `price` numeric(10,2) — Цена товара в рублях; `stock` integer — Остаток на складе, штук

**Колонки ответа:** `naimenovanie`, `cena`, `ostatok`

**Пример ответа (первые строки):**

| naimenovanie | cena | ostatok |
|---|---|---|
| Когтеточка Башня | 2490.00 | 12 |
| Корм Сухой Индейка 1кг | 790.50 | 40 |
| Игрушка Мышка с мятой | 149.00 | 200 |
| Лежанка Гнёздышко | 1290.00 | 8 |
| Лоток Закрытый | 1890.00 | 15 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/gen-m2l1-anatomy-product-aliases?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 14. Товары до 1000 рублей

*лёгкая* · Диалекты: PostgreSQL

В таблице `products` хранится каталог товаров магазина «Котомаркет». Маркетолог готовит подборку «Бюджетные находки» и хочет показать только недорогие товары.

Выведите название, цену и категорию всех товаров, цена которых **строго меньше** 1000 рублей. Для каждого подходящего товара верните колонки `title`, `price`, `category` именно в этом порядке.

Используйте только `SELECT` и `WHERE` со сравнением — без сортировки, группировки и других конструкций.

**Таблицы:**

- **products**: `product_id` integer 🔑 — Идентификатор товара (первичный ключ); `title` text — Название товара; `category` text — Категория товара (мебель, корм, игрушки, аксессуары, уход); `price` integer — Цена товара в рублях; `in_stock` integer — Количество товара на складе

**Колонки ответа:** `title`, `price`, `category`

**Пример ответа (первые строки):**

| title | price | category |
|---|---|---|
| Корм «Сытый кот» 2кг | 890 | корм |
| Игрушка «Мышка» | 150 | игрушки |
| Шампунь «Чистый мех» | 320 | уход |
| Лакомство «Кусь» | 260 | корм |
| Туннель «Норка» | 990 | игрушки |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/gen-m1l5-affordable-products?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 15. Доставленные заказы

*лёгкая* · Диалекты: PostgreSQL

В маркетплейсе «Котомаркет» все заказы хранятся в плоской таблице `orders`. У каждого заказа есть номер, имя покупателя, город, статус и сумма.

Колонка `status` принимает значения: `'обработка'`, `'в пути'`, `'доставлен'`, `'отменён'`.

Служба поддержки хочет увидеть **только доставленные** заказы, чтобы собрать отзывы у довольных клиентов.

Напишите запрос, который выводит **три** столбца — `order_id`, `customer`, `amount` — только для заказов, у которых `status` равен `'доставлен'`.

Используйте только `SELECT` и `WHERE` с проверкой на равенство. Сортировка не требуется, порядок строк не важен.

**Таблицы:**

- **orders**: `order_id` integer 🔑 — Номер заказа (первичный ключ); `customer` text — Имя покупателя; `city` text — Город доставки; `status` text — Статус заказа: обработка, в пути, доставлен, отменён; `amount` integer — Сумма заказа в рублях

**Колонки ответа:** `order_id`, `customer`, `amount`

**Пример ответа (первые строки):**

| order_id | customer | amount |
|---|---|---|
| 1 | Анна Котова | 2490 |
| 3 | Мария Усова | 1500 |
| 6 | Павел Когтев | 260 |
| 8 | Тимур Хвостов | 3200 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/gen-m1l5-orders-status-delivered?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 16. Карточка клиента: проекция с алиасами

*лёгкая* · Диалекты: PostgreSQL

В «Котомаркете» маркетологи готовят выгрузку клиентов для рассылки и хотят, чтобы заголовки колонок были понятными.

Таблица `customers` содержит данные клиентов магазина.

Выведите для **каждого** клиента три столбца, переименовав их с помощью `AS`:

- `full_name` под именем **`klient`**;
- `city` под именем **`gorod`**;
- `signup_date` под именем **`data_registracii`**.

Никакой фильтрации, сортировки или иных преобразований не требуется — только проекция нужных столбцов с алиасами.

**Таблицы:**

- **customers**: `id` integer 🔑 — Идентификатор клиента (первичный ключ); `full_name` text — Полное имя клиента; `city` text — Город клиента; `signup_date` date — Дата регистрации клиента

**Колонки ответа:** `klient`, `gorod`, `data_registracii`

**Пример ответа (первые строки):**

| klient | gorod | data_registracii |
|---|---|---|
| Анна Котова | Москва | 2024-01-12 |
| Игорь Лапкин | Санкт-Петербург | 2024-02-03 |
| Мария Усова | Казань | 2024-02-21 |
| Олег Мурзин | Новосибирск | 2024-03-15 |
| Дарья Пушистова | Екатеринбург | 2024-04-01 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/gen-m2l1-customers-projection?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 17. Товары с двух складов

*лёгкая* · Диалекты: PostgreSQL

В таблице `tovary` маркетплейса «Котомаркет» хранятся товары и города, где находятся их склады.

Менеджер просит показать товары, которые лежат на складе **в Москве** или **в Санкт-Петербурге** — чтобы спланировать доставку по двум столицам.

Выведите колонки `id`, `nazvanie`, `gorod_sklada`, `cena` для товаров, у которых `gorod_sklada` равен `'Москва'` **или** `'Санкт-Петербург'`.

Порядок строк не важен.

**Таблицы:**

- **tovary**: `id` integer 🔑 — Идентификатор товара; `nazvanie` text — Название товара; `gorod_sklada` text — Город, где находится склад с товаром; `cena` integer — Цена товара в рублях

**Колонки ответа:** `id`, `nazvanie`, `gorod_sklada`, `cena`

**Пример ответа (первые строки):**

| id | nazvanie | gorod_sklada | cena |
|---|---|---|---|
| 1 | Когтеточка "Башня" | Москва | 2400 |
| 3 | Игрушка-мышка | Санкт-Петербург | 150 |
| 5 | Шлейка для кота | Москва | 600 |
| 7 | Домик-будка | Санкт-Петербург | 3100 |
| 9 | Переноска "Сафари" | Москва | 1800 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/gen-m2l2-where-or-sklady?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 18. Каталог без архива

*лёгкая* · Диалекты: PostgreSQL

В таблице `cat_products` хранится каталог товаров магазина «Котомаркет». Часть товаров уже снята с продажи и помечена категорией `'архив'` — их не нужно показывать покупателям.

Выведите все товары, **кроме** тех, что лежат в категории `'архив'`. Для каждого подходящего товара верните колонки `product_id`, `name`, `category`, `price`.

Используйте только `SELECT` и `WHERE` — без сортировки, группировки и других конструкций.

**Таблицы:**

- **cat_products**: `product_id` integer 🔑 — Идентификатор товара (первичный ключ); `name` text — Название товара; `category` text — Категория товара (мебель, корм, игрушки, аксессуары, архив); `price` integer — Цена товара в рублях; `in_stock` integer — Количество на складе

**Колонки ответа:** `product_id`, `name`, `category`, `price`

**Пример ответа (первые строки):**

| product_id | name | category | price |
|---|---|---|---|
| 1 | Когтеточка «Башня» | мебель | 2490 |
| 2 | Корм «Сытый кот» 2кг | корм | 890 |
| 3 | Игрушка «Мышка» | игрушки | 150 |
| 4 | Лежанка «Облако» | мебель | 1790 |
| 6 | Лакомство «Кусь» | корм | 260 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/gen-m2l2-where-exclude-archive?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 19. Витрина склада: артикул, вес и цена с понятными именами

*лёгкая* · Диалекты: PostgreSQL

На складе «Котомаркета» товары лежат в плоской таблице `goods`. Колонки названы по-техничному, и менеджеру витрины их трудно читать.

Выбери из таблицы `goods` **ровно три** столбца и подпиши каждый человеческим именем через `AS`:

| Из таблицы | Алиас в результате |
|------------|--------------------|
| `sku`      | `artikul`          |
| `weight_g` | `ves`              |
| `price`    | `cena`             |

Верни **все строки** таблицы (без фильтров и без сортировки). Порядок строк значения не имеет.

Это чистая проекция: ничего, кроме выбора нужных столбцов и их переименования, делать не нужно — никаких `WHERE`, `ORDER BY`, `DISTINCT`.

**Таблицы:**

- **goods**: `sku` text 🔑 — Артикул товара на складе (первичный ключ); `title` text — Название товара; `weight_g` integer — Вес товара в граммах; `price` numeric(10,2) — Цена товара в рублях; `shelf` text — Код полки на складе

**Колонки ответа:** `artikul`, `ves`, `cena`

**Пример ответа (первые строки):**

| artikul | ves | cena |
|---|---|---|
| KM-001 | 1500 | 549.00 |
| KM-002 | 3200 | 1290.00 |
| KM-003 | 45 | 99.50 |
| KM-004 | 800 | 1790.00 |
| KM-005 | 120 | 219.00 |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/gen-m2l1-goods-projection-as?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 20. Отзывы без оценки прочь, пустые комментарии — заглушкой

*лёгкая* · Диалекты: PostgreSQL

В «Котомаркете» покупатели оставляют отзывы на товары. Таблица `reviews` плоская: один отзыв — одна строка. Не каждый отзыв заполнен полностью: иногда покупатель не поставил оценку (`rating` равен `NULL`), а иногда не написал текст (`comment` равен `NULL`).

Команда модерации готовит ленту отзывов и просит сделать выгрузку по двум правилам:

1. Показать **только** отзывы, в которых **есть оценка** — то есть `rating` **не** равен `NULL`. Отзывы без оценки в выгрузку не попадают.
2. Если у отзыва **нет текста** (`comment` равен `NULL`), вместо пустого значения нужно вывести строку-заглушку `'нет комментария'`. Если текст есть — вывести его как есть.

Выведите три столбца: `id`, `product` и текст комментария под именем `comment_text`.

Используйте `IS NOT NULL` для фильтра и `COALESCE` для подстановки заглушки. Сортировка не требуется — порядок строк не важен.

**Таблицы:**

- **reviews**: `id` integer 🔑 — Идентификатор отзыва (первичный ключ); `product` text — Название товара, на который оставлен отзыв; `author` text — Имя автора отзыва; может быть NULL, если отзыв анонимный; `rating` integer — Оценка товара от 1 до 5; NULL, если покупатель не поставил оценку; `comment` text — Текст комментария; NULL, если покупатель не написал текст

**Колонки ответа:** `id`, `product`, `comment_text`

**Пример ответа (первые строки):**

| id | product | comment_text |
|---|---|---|
| 1 | Когтеточка «Башня» | Кот в восторге, точит каждый день |
| 2 | Корм «Сытый кот» 2кг | нет комментария |
| 3 | Игрушка «Мышка» | Любимая игрушка! |
| 5 | Шлейка «Прогулка» | нет комментария |
| 7 | Витамины «Бодрость» | Шерсть стала блестящей |

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/gen-m2l3-reviews-null-coalesce?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**
