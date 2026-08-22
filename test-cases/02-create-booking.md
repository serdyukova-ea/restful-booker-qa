# Создание бронирования — Test Cases

## Endpoint
`POST /booking`

## TC-CREATE-001 — Создание бронирования с валидными данными

**Priority:** High  
**Type:** Positive  
**Endpoint:** `POST /booking`

### Предусловия
- Restful Booker API доступен.
- Подготовлены валидные данные для создания бронирования.

### Тестовые данные
```json
{
  "firstname": "Jim",
  "lastname": "Brown",
  "totalprice": 111,
  "depositpaid": true,
  "bookingdates": {
    "checkin": "2026-09-01",
    "checkout": "2026-09-10"
  },
  "additionalneeds": "Breakfast"
}
```

### Шаги
1. Отправить `POST` запрос на `/booking` с валидными данными.
2. Проверить HTTP status code.
3. Проверить структуру response body.
4. Проверить наличие bookingid.
5. Проверить наличие объекта booking.
6. Сравнить данные в response с данными, переданными в request.

### Ожидаемый результат
1. API возвращает успешный HTTP status code.
2. Response содержит bookingid.
3. bookingid является числовым идентификатором созданного бронирования.
4. Response содержит объект booking.
5. Значения полей в объекте booking соответствуют данным из request.

### Результат выполнения

**Статус:** Passed

**Фактический результат:**

API вернул ответ со статусом 200. В response присутствуют `bookingid` и объект `booking`. Значения полей созданного бронирования соответствуют данным, переданным в запросе.

## TC-CREATE-002 — Создание бронирования с минимальным набором данных

**Priority:** High  
**Type:** Positive / Boundary

### Предусловия
- Restful Booker API доступен.

### Тестовые данные
```json
{
  "firstname": "Jim",
  "lastname": "Brown",
  "totalprice": 100,
  "depositpaid": false,
  "bookingdates": {
    "checkin": "2026-09-01",
    "checkout": "2026-09-10"
  }
}
```

### Шаги
1. Отправить `POST` запрос на `/booking` с минимальным набором данных.
2. Проверить HTTP status code.
3. Проверить response body.
4. Проверить наличие bookingid.
5. Проверить сохранение переданных значений.

### Ожидаемый результат
1. Бронирование успешно создано.
2. Response содержит bookingid.
3. Переданные значения сохранены корректно.
4. Отсутствие необязательного поля additionalneeds не препятствует созданию бронирования.

## TC-CREATE-003 — Создание бронирования со всеми доступными полями

**Priority:** Medium  
**Type:** Positive

### Предусловия
- Restful Booker API доступен.

### Тестовые данные
Использовать валидные значения для всех доступных полей:
- `firstname`
- `lastname`
- `totalprice`
- `depositpaid`
- `bookingdates.checkin`
- `bookingdates.checkout`
- `additionalneeds`

### Шаги
1. Отправить `POST` запрос на `/booking`.
2. Проверить HTTP status code.
3. Проверить структуру response body.
4. Сравнить все переданные поля с данными в response.

### Ожидаемый результат
1. Бронирование успешно создано.
2. Все переданные значения корректно сохранены и возвращены в response.

## TC-CREATE-004 — Создание бронирования с отрицательным значением totalprice

**Priority:** Medium  
**Type:** Negative / Validation

### Предусловия

- Restful Booker API доступен.

### Тестовые данные

```json
{
  "firstname": "Jim",
  "lastname": "Brown",
  "totalprice": -1,
  "depositpaid": true,
  "bookingdates": {
    "checkin": "2026-09-01",
    "checkout": "2026-09-10"
  }
}
```
### Шаги
1. Отправить `POST` запрос на `/booking` с отрицательным значением `totalprice`.
2. Проверить HTTP status code.
3. Проверить response body.
4. Проверить, было ли создано бронирование.

### Ожидаемый результат
1. API отклоняет некорректное значение totalprice.
2. Бронирование с отрицательной стоимостью не создаётся.
3. API возвращает соответствующий HTTP status code и сообщение об ошибке.

## TC-CREATE-005 — Передача строкового значения в поле totalprice

**Priority:** Medium  
**Type:** Negative / Validation

### Тестовые данные
```json
{
  "firstname": "Jim",
  "lastname": "Brown",
  "totalprice": "one hundred",
  "depositpaid": true,
  "bookingdates": {
    "checkin": "2026-09-01",
    "checkout": "2026-09-10"
  }
}
```
### Шаги
1. Отправить `POST` запрос на `/booking` со строковым значением в `totalprice`.
2. Проверить HTTP status code.
3. Проверить response body.
4. Проверить, было ли создано бронирование.

### Ожидаемый результат
1. API отклоняет значение некорректного типа.
2. Бронирование не создаётся.
3. Response содержит информацию об ошибке валидации.


## TC-CREATE-006 — Создание бронирования с датой checkout раньше даты checkin

**Priority:** High  
**Type:** Negative / Business validation

### Тестовые данные
```json
{
  "firstname": "Jim",
  "lastname": "Brown",
  "totalprice": 100,
  "depositpaid": true,
  "bookingdates": {
    "checkin": "2026-09-10",
    "checkout": "2026-09-01"
  }
}
```
### Шаги
1. Отправить `POST` запрос на `/booking` с переданным `checkout`, который предшествует `checkin`.
2. Проверить HTTP status code.
3. Проверить response body.
4. Проверить, было ли создано бронирование.

### Ожидаемый результат
1. API отклоняет бронирование с некорректным диапазоном дат.
2. Бронирование не создаётся.
3. Response содержит информацию об ошибке валидации.
