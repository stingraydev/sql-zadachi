# Задачи по SQL с онлайн-проверкой

99 практических задач по SQL — от `SELECT` и `WHERE` до оконных функций, CTE и изменения структуры таблиц. Подойдут, чтобы научиться писать запросы с нуля, подтянуть JOIN и GROUP BY или подготовиться к собеседованию на аналитика данных, разработчика или тестировщика.

У каждой задачи есть рабочий контекст, схема таблиц и пример ожидаемого ответа. Решать их удобнее всего в онлайн-тренажёре **[SQL Arena](https://sql.coderang.dev/?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)**: пишете запрос в браузере, нажимаете «Отправить» — и ответ сразу проверяется на скрытых данных. Ничего устанавливать не нужно, задачи работают на PostgreSQL, а многие ещё на MySQL и ClickHouse.

## Темы

| Тема | Задач |
|---|---|
| [SELECT, WHERE, ORDER BY — выборка и фильтрация](tasks/01-select-where-order-by.md) | 20 |
| [Агрегатные функции и GROUP BY](tasks/02-agregaty-group-by.md) | 18 |
| [JOIN — соединение таблиц](tasks/03-join.md) | 18 |
| [Подзапросы](tasks/04-podzaprosy.md) | 9 |
| [CTE (WITH) — общие табличные выражения](tasks/05-cte-with.md) | 8 |
| [Оконные функции](tasks/06-okonnye-funkcii.md) | 14 |
| [INSERT, UPDATE, DELETE — изменение данных](tasks/07-insert-update-delete.md) | 6 |
| [CREATE и ALTER TABLE — структура таблиц](tasks/08-create-alter-table.md) | 6 |

## Как устроена задача

- **Условие** — короткая рабочая ситуация: что нужно узнать и в каком виде вывести.
- **Таблицы** — колонки, типы, первичные (🔑) и внешние (→) ключи.
- **Колонки ответа и пример** — какие поля ждёт проверка и как выглядят первые строки правильного результата.
- **Ссылка «Решить онлайн»** — задача в тренажёре: редактор, песочница с данными и автоматическая проверка.

Готовых решений здесь нет намеренно: задача, к которой подсмотрен ответ, ничему не учит. Тренажёр сравнит ваш запрос с эталоном на данных, которых вы не видите, и подскажет, в чём расхождение: лишние строки, не те колонки, неверный порядок.

## Все задачи

### [SELECT, WHERE, ORDER BY — выборка и фильтрация](tasks/01-select-where-order-by.md)

1. [Лекарства, которые продаются без рецепта](https://sql.coderang.dev/trainer/tasks/pharma-1?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
2. [Количество клиентов из Берлина](https://sql.coderang.dev/trainer/tasks/pharma-2?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
3. [Платиновые участники программы лояльности](https://sql.coderang.dev/trainer/tasks/loyal-1?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
4. [Количество дальних рейсов](https://sql.coderang.dev/trainer/tasks/loyal-2?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
5. [Фитнес-клубы в Берлине](https://sql.coderang.dev/trainer/tasks/fit-1?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
6. [Количество Premium-клиентов](https://sql.coderang.dev/trainer/tasks/fit-2?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
7. [Пятизвёздочные отели сети](https://sql.coderang.dev/trainer/tasks/hotel-1?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
8. [Рок-артисты фестивальной базы](https://sql.coderang.dev/trainer/tasks/fest-1?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
9. [Количество просторных номеров](https://sql.coderang.dev/trainer/tasks/hotel-2?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
10. [Количество фестивалей в 2024 году](https://sql.coderang.dev/trainer/tasks/fest-2?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
11. [Виды животных на грани исчезновения](https://sql.coderang.dev/trainer/tasks/zoo-1?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
12. [Количество животных в секции Africa Savanna](https://sql.coderang.dev/trainer/tasks/zoo-2?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
13. [Витрина товаров: переименуй колонки](https://sql.coderang.dev/trainer/tasks/gen-m2l1-anatomy-product-aliases?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
14. [Товары до 1000 рублей](https://sql.coderang.dev/trainer/tasks/gen-m1l5-affordable-products?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
15. [Доставленные заказы](https://sql.coderang.dev/trainer/tasks/gen-m1l5-orders-status-delivered?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
16. [Карточка клиента: проекция с алиасами](https://sql.coderang.dev/trainer/tasks/gen-m2l1-customers-projection?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
17. [Товары с двух складов](https://sql.coderang.dev/trainer/tasks/gen-m2l2-where-or-sklady?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
18. [Каталог без архива](https://sql.coderang.dev/trainer/tasks/gen-m2l2-where-exclude-archive?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
19. [Витрина склада: артикул, вес и цена с понятными именами](https://sql.coderang.dev/trainer/tasks/gen-m2l1-goods-projection-as?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
20. [Отзывы без оценки прочь, пустые комментарии — заглушкой](https://sql.coderang.dev/trainer/tasks/gen-m2l3-reviews-null-coalesce?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая

### [Агрегатные функции и GROUP BY](tasks/02-agregaty-group-by.md)

21. [Пульс продаж по месяцам](https://sql.coderang.dev/trainer/tasks/dtm-monthly-sales-pulse?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
22. [Часы прослушивания по месяцам](https://sql.coderang.dev/trainer/tasks/dtm-streaming-monthly-hours?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
23. [Сводка доставки по магазинам](https://sql.coderang.dev/trainer/tasks/aag-store-delivery-scorecard?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
24. [Первый цифровой след клиента](https://sql.coderang.dev/trainer/tasks/ret-first-banking-activity?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
25. [Двойная регистрация одной посылки](https://sql.coderang.dev/trainer/tasks/dqa-duplicate-parcel-business-keys?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
26. [Частота покупок в аудиосервисе](https://sql.coderang.dev/trainer/tasks/rfm-quarterly-purchase-frequency?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
27. [Кого пора возвращать в маркетплейс](https://sql.coderang.dev/trainer/tasks/rfm-client-recency-as-of-date?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
28. [От заявки до одобрения KYC](https://sql.coderang.dev/trainer/tasks/fun-kyc-submit-to-approval?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
29. [Самые читаемые книги библиотеки](https://sql.coderang.dev/trainer/tasks/ai-1775636066836-hemq?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
30. [Помесячный отчёт по заказам Котомаркета](https://sql.coderang.dev/trainer/tasks/gen-g6l5-monthly-orders-report?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
31. [Топ-3 категории товаров по выручке](https://sql.coderang.dev/trainer/tasks/ai-1777187603534-aok0?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
32. [Средняя зарплата по отделам за 2023 год](https://sql.coderang.dev/trainer/tasks/ai-1777187735180-c7kf?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
33. [Доходные жанры книжного магазина](https://sql.coderang.dev/trainer/tasks/ai-1775635279697-f1bp?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
34. [Анализ производительности курьеров по доставленным посылкам](https://sql.coderang.dev/trainer/tasks/ai-1781871231464-fsst?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
35. [Клиенты с покупками на сумму больше 500](https://sql.coderang.dev/trainer/tasks/ai-1775670901436-66td?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
36. [Доходные категории товаров](https://sql.coderang.dev/trainer/tasks/ai-1775641700820-h25c?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
37. [Кассовые сборы популярных жанров](https://sql.coderang.dev/trainer/tasks/ai-1784269947391-uk7v?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
38. [Самые плодовитые авторы с высоким рейтингом](https://sql.coderang.dev/trainer/tasks/ai-1783004573963-aiwb?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя

### [JOIN — соединение таблиц](tasks/03-join.md)

39. [Полки второго уровня](https://sql.coderang.dev/trainer/tasks/rct-store-direct-subcategories?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
40. [Один к одному, один ко многим](https://sql.coderang.dev/trainer/tasks/jcr-academy-relations?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
41. [Размножение строк после JOIN](https://sql.coderang.dev/trainer/tasks/jcr-stream-fanout?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
42. [Пары сопоставимых квартир](https://sql.coderang.dev/trainer/tasks/lsa-district-listing-pairs?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
43. [Сотрудники и их отделы](https://sql.coderang.dev/trainer/tasks/ai-1775637019643-eunn?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
44. [Популярные автомобили с несколькими бронированиями](https://sql.coderang.dev/trainer/tasks/ai-1777261814660-zi32?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
45. [Первые пять посылок в пути](https://sql.coderang.dev/trainer/tasks/ai-1778256950814-4sv2?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
46. [Топ игроки с высокой средней оценкой](https://sql.coderang.dev/trainer/tasks/ai-1779047665720-a2sr?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
47. [Анализ прибыльности маршрутов авиакомпании](https://sql.coderang.dev/trainer/tasks/ai-1782644485879-37vn?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
48. [Товары с высоким оборотом и рентабельностью](https://sql.coderang.dev/trainer/tasks/ai-1787750925236-chyg?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
49. [Самые активные авторы по количеству опубликованных статей](https://sql.coderang.dev/trainer/tasks/ai-1787751852906-h5a1?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
50. [Загруженные отделения клиники](https://sql.coderang.dev/trainer/tasks/ai-1791184175847-gz7f?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
51. [Лучшие гостиничные номера по среднему рейтингу и доходу](https://sql.coderang.dev/trainer/tasks/ai-1789653316245-yp2u?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
52. [Топ компании по среднему рейтингу отзывов соискателей](https://sql.coderang.dev/trainer/tasks/ai-1785332014250-r4f3?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
53. [Прибыльные номера отеля за квартал](https://sql.coderang.dev/trainer/tasks/ai-1789563056453-x45d?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
54. [Врачи с максимальной нагрузкой пациентов](https://sql.coderang.dev/trainer/tasks/ai-1787905556716-aupk?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
55. [Анализ убыточности страховых полисов по регионам](https://sql.coderang.dev/trainer/tasks/ai-1790319194211-v0bh?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
56. [Урожайность фермеров-лидеров по культурам](https://sql.coderang.dev/trainer/tasks/ai-1787822297972-f1yr?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя

### [Подзапросы](tasks/04-podzaprosy.md)

57. [Самые дорогие товары каталога](https://sql.coderang.dev/trainer/tasks/easy-subq-most-expensive-product?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
58. [Заказы российских клиентов](https://sql.coderang.dev/trainer/tasks/easy-subq-orders-from-ru-customers?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
59. [Заказы выше среднего оплаченного чека](https://sql.coderang.dev/trainer/tasks/easy-subq-orders-above-avg?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
60. [Клиенты, которые уже оформляли заказы](https://sql.coderang.dev/trainer/tasks/easy-subq-customers-with-orders?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
61. [Товары без единой продажи](https://sql.coderang.dev/trainer/tasks/easy-subq-products-never-ordered?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
62. [Количество заказов у каждого клиента](https://sql.coderang.dev/trainer/tasks/easy-subq-order-count-per-customer?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
63. [Самый доступный товар в каждой категории](https://sql.coderang.dev/trainer/tasks/easy-subq-cheapest-per-category?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
64. [Сканы посылок после watermark](https://sql.coderang.dev/trainer/tasks/etl-watermark-parcel-scans?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
65. [Зрители документалок](https://sql.coderang.dev/trainer/tasks/lsa-documentary-watchers?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая

### [CTE (WITH) — общие табличные выражения](tasks/05-cte-with.md)

66. [Топовые клиенты банка по сумме транзакций](https://sql.coderang.dev/trainer/tasks/ai-1777242925149-2xrk?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — сложная
67. [Поквартальная эффективность менеджеров продаж](https://sql.coderang.dev/trainer/tasks/ai-1775635598933-m421?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — сложная
68. [Топ курьеры по доставкам с учётом срочности](https://sql.coderang.dev/trainer/tasks/ai-1777263423404-9c2a?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — сложная
69. [Топ-3 сотрудников по суммарному доходу в каждом отделе](https://sql.coderang.dev/trainer/tasks/ai-1775671119763-2ukv?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — сложная
70. [Хиты месяца по новым трекам в плейлистах](https://sql.coderang.dev/trainer/tasks/ai-1775675622104-qs7d?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — сложная
71. [Топ-5 самых прослушиваемых артистов в плейлистах](https://sql.coderang.dev/trainer/tasks/ai-1775675459674-b6li?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — сложная
72. [Рейтинг успеваемости студентов по кафедрам с динамикой оценок](https://sql.coderang.dev/trainer/tasks/ai-1788857992408-sa5x?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — сложная
73. [Рост выручки месяц к месяцу](https://sql.coderang.dev/trainer/tasks/ai-1775673452252-fuqx?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — сложная

### [Оконные функции](tasks/06-okonnye-funkcii.md)

74. [Паузы между прослушиваниями](https://sql.coderang.dev/trainer/tasks/ses-stream-play-gaps?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
75. [Флаг начала сессии в интернет-магазине](https://sql.coderang.dev/trainer/tasks/ses-shop-session-flag?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
76. [Операционный баланс необанка](https://sql.coderang.dev/trainer/tasks/wfr-neobank-running-balance?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
77. [Доля каждого товара в общей выручке через SUM() OVER ()](https://sql.coderang.dev/trainer/tasks/gen-m7l1-window-share-of-total?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
78. [Зарплаты сотрудников: насколько выше или ниже среднего](https://sql.coderang.dev/trainer/tasks/gen-m7l1b-staff-salary-vs-average?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
79. [Рейтинг студентов по средней оценке внутри специальности](https://sql.coderang.dev/trainer/tasks/ai-1778004364778-0tho?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
80. [Урожайность по сортам культур с рангированием](https://sql.coderang.dev/trainer/tasks/ai-1786790300439-tv0i?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
81. [Читатели-рекордсмены по жанрам](https://sql.coderang.dev/trainer/tasks/ai-1790350306207-8sq5?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — сложная
82. [Динамика выплат по страховым полисам](https://sql.coderang.dev/trainer/tasks/ai-1790535919225-byut?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — сложная
83. [Динамика платежей участников фитнес-клуба](https://sql.coderang.dev/trainer/tasks/ai-1790360193402-040t?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — сложная
84. [Прирост выручки автопарка по месяцам](https://sql.coderang.dev/trainer/tasks/ai-1790361107661-qhhp?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — сложная
85. [Кассовые рекорды кинозала по месяцам](https://sql.coderang.dev/trainer/tasks/ai-1790478543031-ofx6?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — сложная
86. [Восходящие звёзды тревел-агентства](https://sql.coderang.dev/trainer/tasks/ai-1790481334663-qe95?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — сложная
87. [Динамика повторных визитов пациентов к врачам](https://sql.coderang.dev/trainer/tasks/ai-1789731153744-4c8k?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — сложная

### [INSERT, UPDATE, DELETE — изменение данных](tasks/07-insert-update-delete.md)

88. [Скидка на игры жанра Action](https://sql.coderang.dev/trainer/tasks/discount-action-games?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
89. [Засидить тестовые заказы с разными статусами](https://sql.coderang.dev/trainer/tasks/qa-seed-test-orders?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
90. [Удалить все незакреплённые заметки](https://sql.coderang.dev/trainer/tasks/easy-dml-delete-unpinned?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
91. [Добавить первую заметку в дневник](https://sql.coderang.dev/trainer/tasks/easy-dml-insert-note?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
92. [Закрепить все январские заметки 2024 года](https://sql.coderang.dev/trainer/tasks/easy-dml-pin-old-notes?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
93. [Добавить тестового пользователя в баг-трекер](https://sql.coderang.dev/trainer/tasks/qa-insert-test-user?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая

### [CREATE и ALTER TABLE — структура таблиц](tasks/08-create-alter-table.md)

94. [Удалить таблицу departments](https://sql.coderang.dev/trainer/tasks/ddl-drop-departments?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
95. [Добавить email сотрудника](https://sql.coderang.dev/trainer/tasks/ddl-add-email-column?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
96. [Удалить столбец salary из employees](https://sql.coderang.dev/trainer/tasks/ddl-drop-salary-column?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
97. [Переименовать столбец name в full_name](https://sql.coderang.dev/trainer/tasks/ddl-rename-name-column?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — лёгкая
98. [Нормализация: разнести каталог книг в authors + books (PK/FK)](https://sql.coderang.dev/trainer/tasks/gen-m9l5-normalize-books-authors?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя
99. [Котомаркет: разнести заказ в 3НФ](https://sql.coderang.dev/trainer/tasks/gen-ddll5-orders-3nf-split?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) — средняя

## Больше задач

Здесь 99 задач из открытой части тренажёра. В [SQL Arena](https://sql.coderang.dev/trainer/tasks?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi) их больше 1 400: задачи с собеседований, курс SQL с нуля, курсы по аналитике, ClickHouse и Kafka, дуэли и рейтинг.

---

[English version → sql-practice-problems](https://github.com/stingraydev/sql-practice-problems)

© SQL Arena, [sql.coderang.dev](https://sql.coderang.dev/?utm_source=github&utm_medium=repo&utm_campaign=sql-zadachi)
