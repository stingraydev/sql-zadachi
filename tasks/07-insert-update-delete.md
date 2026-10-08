# INSERT, UPDATE, DELETE — изменение данных

[← Ко всем темам](../README.md)

## 88. Скидка на игры жанра Action

*лёгкая* · Диалекты: PostgreSQL, MySQL

На выходных магазин запускает акцию: скидка 10% на все игры жанра `Action`. Обновите цены этих игр в каталоге: каждая такая цена должна быть умножена на `0.9`.

**Таблицы:**

- **players**: `id` int 🔑 — Идентификатор игрока; `name` varchar(100) — Имя игрока; `email` varchar(255) — Электронная почта; `city` varchar(100) — Город игрока; `registered_at` date — Дата регистрации
- **games**: `id` int 🔑 — Идентификатор игры; `title` varchar(200) — Название игры; `genre` varchar(100) — Жанр игры; `price` decimal(10,2) — Цена игры; `stock` int — Остаток на складе
- **orders**: `id` int 🔑 — Идентификатор заказа; `player_id` int → players.id — Идентификатор игрока; `created_at` timestamp — Дата создания заказа; `status` varchar(20) — Статус заказа
- **order_items**: `id` int 🔑 — Идентификатор позиции заказа; `order_id` int → orders.id — Идентификатор заказа; `game_id` int → games.id — Идентификатор игры; `quantity` int — Количество; `price` decimal(10,2) — Цена за единицу

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/discount-action-games?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 89. Засидить тестовые заказы с разными статусами

*лёгкая* · Диалекты: PostgreSQL, MySQL

Чтобы прогнать сценарии обработки заказов в разных состояниях, нужно подготовить тестовые данные. Вставьте в таблицу `orders` одним запросом три строки для пользователя `user_id = 1`: заказ `501` со статусом `PAID` и суммой `100.00`, заказ `502` со статусом `PENDING` и суммой `250.00`, заказ `503` со статусом `CANCELLED` и суммой `75.50`. Для поля `created_at` используйте `CURRENT_TIMESTAMP`.

**Таблицы:**

- **users**: `id` int 🔑 — Идентификатор пользователя; `email` varchar(255) — Электронная почта пользователя
- **orders**: `id` int 🔑 — Идентификатор заказа; `user_id` int → users.id — Идентификатор пользователя; `status` varchar(20) — Статус заказа; `amount` decimal(10,2) — Сумма заказа; `created_at` timestamp — Дата создания заказа

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/qa-seed-test-orders?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 90. Удалить все незакреплённые заметки

*лёгкая* · Диалекты: PostgreSQL

Пользователь делает «весеннюю уборку» в дневнике: всё, что не было закреплено вручную, считается лишним шумом. Удалите из таблицы `notes` все строки, у которых `is_pinned = FALSE`. Закреплённые заметки (`is_pinned = TRUE`) должны остаться.

**Таблицы:**

- **notes**: `id` serial 🔑 — Идентификатор заметки; `title` varchar(120) — Заголовок заметки; `body` text — Текст заметки; `is_pinned` boolean — Признак закрепления; `created_at` date — Дата создания заметки

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/easy-dml-delete-unpinned?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 91. Добавить первую заметку в дневник

*лёгкая* · Диалекты: PostgreSQL

Вы разрабатываете приложение-дневник в духе Notion и хотите проверить, что добавление новой записи работает корректно. Сохраните в таблицу `notes` одну заметку: в `title` запишите `Привет SQL`, а в `body` — `Первая запись через INSERT`. Поля `id`, `is_pinned` и `created_at` не передавайте: они должны заполниться значениями по умолчанию.

**Таблицы:**

- **notes**: `id` serial 🔑 — Идентификатор заметки; `title` varchar(120) — Заголовок заметки; `body` text — Текст заметки; `is_pinned` boolean — Признак закрепления; `created_at` date — Дата создания заметки

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/easy-dml-insert-note?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 92. Закрепить все январские заметки 2024 года

*лёгкая* · Диалекты: PostgreSQL

К новому году пользователь решил поднять наверх все январские заметки за 2024 год: они оказались самыми полезными. В таблице `notes` установите `is_pinned = TRUE` для всех строк, у которых `created_at` попадает в январь 2024 года включительно. Даты `2024-01-01` и `2024-01-31` тоже должны входить в диапазон. Остальные заметки не меняйте.

**Таблицы:**

- **notes**: `id` serial 🔑 — Идентификатор заметки; `title` varchar(120) — Заголовок заметки; `body` text — Текст заметки; `is_pinned` boolean — Признак закрепления; `created_at` date — Дата создания заметки

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/easy-dml-pin-old-notes?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**

---

## 93. Добавить тестового пользователя в баг-трекер

*лёгкая* · Диалекты: PostgreSQL, MySQL

В тестовом окружении баг-трекера нужно завести аккаунт тестировщика, чтобы проверять сценарии с ролью tester. Добавьте в таблицу `users` новую запись со следующими значениями: `id = 101`, `email = 'qa.test@example.com'`, `role_id = 1`, `is_active = true`, `created_at = CURRENT_TIMESTAMP`.

**Таблицы:**

- **roles**: `id` int 🔑 — Идентификатор роли; `name` varchar(50) — Название роли
- **users**: `id` int 🔑 — Идентификатор пользователя; `email` varchar(255) — Электронная почта пользователя; `role_id` int → roles.id — Идентификатор роли; `is_active` boolean — Признак активности; `created_at` timestamp — Дата создания

**[▶ Решить онлайн с автопроверкой](https://sql.coderang.dev/trainer/tasks/qa-insert-test-user?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**
