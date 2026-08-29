# Проверка корректности фильтрации — Test Cases

## Base URL: https://restful-booker.herokuapp.com

## Endpoint
`GET /booking`

## Тестовые сценарии
- Фильтрация по несуществующему значению
- Фильтрация по пустому значению
  
---

## TC-FILTER-001 — Фильтрация по несуществующему значению

**Priority:** High  
**Type:** Functional / Negative  
**Method:** `GET`  
**Endpoint:** `/booking?firstname={Любое несуществующее имя}`

### Предусловия
- Restful Booker API доступен.

### Тестовые данные
`/booking?firstname=Неттакогоимени`

### Шаги
1. Отправить `GET` запрос на `/booking?firstname={Любое несуществующее имя}`.
2. Проверить HTTP status code.
3. Проверить response body.

### Ожидаемый результат
- API возвращает `200 OK`.
- Response содержит пустой массив

### Результат выполнения
**Status:** Passed

**Фактический результат:**
API вернул `200 OK`. Response содержит пустой массив.

## TC-FILTER-002 — Фильтрация по пустому значению

**Priority:** High  
**Type:** Functional / Negative  
**Method:** `GET`  
**Endpoint:** `/booking?lastname=`

### Предусловия
- Restful Booker API доступен.

### Тестовые данные
Не требуются.

### Шаги
1. Отправить `GET` запрос на `/booking?lastname=`.
2. Проверить HTTP status code.
3. Проверить response body.

### Ожидаемый результат
- API возвращает `200 OK`.
- Response содержит пустой массив

### Результат выполнения
**Status:** Passed

**Фактический результат:**
API вернул `200 OK`. Response содержит пустой массив.
