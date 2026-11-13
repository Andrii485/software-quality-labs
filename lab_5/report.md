# Лабораторна робота №5

## Інтеграційне тестування компонентів та зовнішніх систем

**Виконав:** Бондаренко Андрій\
**Група:** 6.1213-пі-2\
**Дата виконання:** 13.11.2026

## 1. Component Integration Testing

### Test Object
`CartService <-> shop-utils`

### Scenario 1 – Discount
Test Data:
- item 1: price = 100;
- item 2: price = 200;
- discount = 10%.

Expected Result: `270`

Actual Result: `270`

Result: `Pass`

### Scenario 2 – Invalid Discount
Test Data:
- item: price = 100;
- discount = 110%.

Expected Result: `Discount must be between 0 and 100`

Actual Result: `Error: Discount must be between 0 and 100`

Result: `Pass` (negative test: очікувана помилка співпала з фактичною)

## 2. System Integration Testing

### Test Object
`ExternalEchoGateway ↔ Postman Echo`

### Test Data
- orderId = `ORD-001`;
- total = `270`.

### Expected Result
```json
{ "orderId": "ORD-001", "total": 270 }
```

### Actual Result
```json
{ "orderId": "ORD-001", "total": 270 }
```

Result: `Pass`

## 3. Підсумок запуску

| Команда | Результат |
|---|---|
| `npx vitest run` | 3 files, 18 passed |
| `npx vitest run integration` | 2 files, 3 passed |

## Висновки

У роботі було розглянуто інтеграційне тестування на двох рівнях і показано, чим воно відрізняється від тестування окремого компонента.

1. Component Integration: без mock перевірено спільну роботу `CartService` і `calculateDiscount()`. Позитивний сценарій дав очікувані 270 (100 + 200 зі знижкою 10%), а в негативному сценарії помилка `Discount must be between 0 and 100`.
2. System Integration: `ExternalEchoGateway` через реальну HTTP-мережу надіслав `orderId` і `total` до Postman Echo та отримав їх назад без спотворень.

Усі 16 тестів пройшли, зокрема 3 інтеграційні. Експеримент без інтернету показав, що лише системний тест падає (`fetch failed`), бо залежить від мережі й DNS. 