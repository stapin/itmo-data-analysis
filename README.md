# Задание на анализ данных
 **Задание**: провести разведочный анализ данных, придумать продуктовые и технические гипотезы — какую ценность можете извлечь из данных для организации, которая предоставила данные.


# Общее описание `transaction_fraud_data.parquet`

Этот анонимизированный набор данных реальных финансовые транзакции, который предназначен для разработки и тестирования моделей выявления мошеннических операций.

Он охватывает различные сценарии — от розничной торговли и ресторанов до путешествий и здравоохранения — и включает как легитимные, так и мошеннические операции. В нём представлены важные признаки, влияющие на распознавание мошенничества: сумма, тип устройства, география, валюта, тип карты и метка `is_fraud`.

## Ключевые особенности

- **Разнообразие категорий**: Розница (онлайн и офлайн), рестораны (фастфуд и премиум), развлечения, здравоохранение, образование, топливо, путешествия и др.
- **География и валюта**: Транзакции охватывают разные страны, города и валюты, что позволяет моделировать глобальные риски.
- **Профили клиентов**: Для каждой транзакции предусмотрены данные о клиенте — возраст аккаунта, используемые устройства, типичные траты, уровень защиты от мошенничества.
- **Данные, готовые для ML**: Признаки включают скорость транзакций, риск вендора, присутствие карты, отпечатки устройств и другие факторы, помогающие обнаруживать подозрительные паттерны.

## Возможные применения

- Построение моделей выявления мошенничества.
- Анализ транзакционного поведения клиентов.
- Разработка и тестирование алгоритмов обнаружения аномалий.
- Изучение методов feature engineering, оценки моделей и оптимизации производительности в сфере финтеха и e-commerce.


# Содержание файла `transaction_fraud_data.parquet`

| Поле | Описание | Тип |
|------|----------|-----|
| `transaction_id` | Уникальный идентификатор транзакции | String | 
| `customer_id` | Уникальный идентификатор клиента | String | 
| `card_number` | Маскированный номер карты | Int64 |
| `timestamp` | Дата и время транзакции | Datetime(time_unit='us') |
| `vendor_category` | Общая категория вендора (например, Розница, Путешествия) | String |
| `vendor_type` | Тип вендора внутри категории (например, "онлайн") | String |
| `vendor` | Название вендора | String |
| `amount` | Сумма транзакции | Float64 |
| `currency` | Валюта (например, USD, EUR, JPY) | String |
| `country` | Страна, где проведена транзакция | String |
| `city` | Город, где проведена транзакция | String |
| `city_size` | Размер города (например, средний, крупный) | String |
| `card_type` | Тип карты (например, Basic Credit, Gold Credit) | String |
| `is_card_present` | Присутствовала ли карта физически при оплате (POS) | Boolean |
| `device` | Устройство, с которого проведена транзакция (например, Chrome, iOS App) | String |
| `channel` | Канал проведения транзакции (веб, мобильный, POS) | String |
| `device_fingerprint` | Уникальный отпечаток устройства | String |
| `ip_address` | IP-адрес транзакции | String | 
| `is_outside_home_country` | Признак того, что операция проведена вне страны клиента | Boolean |
| `is_high_risk_vendor` | Является ли категория вендора рискованной (например, Путешествия, Развлечения) | Boolean |
| `is_weekend` | Произошла ли операция в выходной день | Boolean |
| `last_hour_activity` | Показатели активности за последний час в виде вложенной структуры | Struct({'num_transactions': Int64, 'total_amount': Float64, 'unique_merchants': Int64, 'unique_countries': Int64, 'max_single_amount': Float64}) |
| `is_fraud` | Является ли транзакция мошеннической (`True` / `False`) | Boolean |

Составное поле `last_hour_activity`:

| Ключ | Описание | Тип |
|------|----------|-----|
| `num_transactions` | Количество транзакций | Int64 |
| `total_amount` | Общая сумма транзакций | Float64 |
| `unique_merchants` | Число уникальных продавцов | Int64 |
| `unique_countries` | Число уникальных стран | Int64 |
| `max_single_amount` | Максимальная сумма одной транзакции | Float64 |


# Содержание файла `historical_currency_exchange.parquet`

Вспомогательные данные для перевода операций в нужную валюту.

Обменный курс с `2024-09-30` по `2024-10-30` относительно `USD`.

| Поле | Описание | Тип |
|------|----------|-----|
| `date` | Дата обменного курса | Date | 
| `AUD` | Австралийский доллар | Float64 | 
| `BRL` | Бразильский реал | Float64 |
| `CAD` | Канадский доллар | Float64 |
| `EUR` | Евро | Float64 |
| `GBP` | Британский фунт стерлингов | Float64 |
| `JPY` | Японская иена | Float64 |
| `MXN` | Мексиканское песо | Float64 |
| `NGN` | Нигерийская найра | Float64 |
| `RUB` | Российский Рубль | Float64 |
| `SGD` | Сингапурский доллар | Float64 |
| `USD` | Доллар США | Int64 |
