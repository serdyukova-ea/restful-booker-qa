# BUG-001 — API принимает totalprice с некорректным типом данных

**Серьёзность:** Средняя  
**Приоритет:** Средний  
**Статус:** Открыт  
**Метод:** `POST`  
**Endpoint:** `/booking`

## Краткое описание
API принимает строковое значение в поле `totalprice`, но согласно документации поле должно содержать числовое значение.

## Предусловия
- Restful Booker API доступен.

## Тестовые данные
```json
{
  "firstname": "Ольга",
  "lastname": "Григорьева",
  "totalprice": "one hundred",
  "depositpaid": true,
  "bookingdates": {
    "checkin": "2026-09-09",
    "checkout": "2026-09-10"
  },
  "additionalneeds": "Завтрак на шведском столе"
}
```
## Шаги воспроизведения
1. Отправить `POST /booking`.
2. Передать в поле `totalprice` строковое значение "one hundred".
3. Проверить HTTP status code.
4. Проверить значение `totalprice` в response.
