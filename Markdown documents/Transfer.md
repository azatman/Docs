# Transfer method
[Описание](#описание)

[Логика работы метода](#логика-работы-метода)

[Входные параметры](#входные-параметры)

[Выходные параметры](#выходные-параметры)

[Обработка ошибок](#обработка-ошибок)
## Описание
Метод Transfer предназначен для осуществления операции перевода денежных средств с одного счета на другой. Этот метод широко используется в финансовых приложениях и системах для обеспечения возможности передачи денег между пользователями, а также для выполнения платежей и переводов на банковские карты.

## Логика работы метода
[transfer method.puml](..%2FPlantUML%20diagrams%2Ftransfer%20method.puml)

## Входные параметры
| №   | Параметр       | Формат | Обязательность | Описание                             |
|-----|----------------|--------|----------------|--------------------------------------|
| 1   | amount         | object | +              | Information about amount of transfer |
| 1.1 | value          | number | +              | Value of amount                      |
| 1.2 | currency       | string | +              | Currency of transfer                 |
| 1.3 | symbolCurrency | string | +              | Symbol of currency                   |
| 2   | senderId       | uuid   | +              | Unique identifier for the sender     |
| 3   | senderName     | string | -              | Sender name                          |
| 4   | recipientCard  | string | +              | Recipient card number                |
| 5   | recipientName  | string | -              | Recipient name                       |
| 6   | description    | string | -              | Text description of transfer         |


```
{
  "amount": {
    "value": 2537.73,
    "currency": "Rub",
    "symbolCurrency": "₽"
  },
  "senderId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "senderName": "Ivanov Ivan Ivanovich",
  "recipientCard": "4267345814389798",
  "recipientName": "Petrov Pyotr Petrovich",
  "description": "Happy Birthday Gift"
}
```

## Выходные параметры
| №   | Параметр       | Формат | Обязательность | Описание                             |
|-----|----------------|--------|----------------|--------------------------------------|
| 1   | id             | uuid   | +              | Unique identifier for the transfer   |
| 2   | amount         | object | +              | Information about amount of transfer |
| 2.1 | value          | number | +              | Value of amount                      |
| 2.2 | currency       | string | +              | Currency of transfer                 |
| 2.3 | symbolCurrency | string | +              | Symbol of currency                   |
| 3   | senderId       | uuid   | +              | Unique identifier for the sender     |
| 4   | senderName     | string | -              | Sender name                          |
| 5   | receiverId     | uuid   | +              | Unique identifier for the receiver   |
| 6   | receiverName   | string | -              | Receiver name                        |
| 7   | description    | string | -              | Text description of transfer         |
| 8   | status         | enum   | +              | Status of transfer                   |

```
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "amount": {
    "value": 2537.73,
    "currency": "Rub",
    "symbolCurrency": "₽"
  },
  "senderId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "senderName": "Ivanov Ivan Ivanovich",
  "recipientCard": "4267345814389798",
  "recipientName": "Petrov Pyotr Petrovich",
  "description": "Happy Birthday Gift",
  "status": "Created"
}
```
## Обработка ошибок
### 400 Bad Request
В случае некорректных данных запроса (Недостаточно средств на счете, Ошибка в номере карты) или отсутствия обязательных полей будет возвращен ответ с кодом ошибки 400 и следующим JSON-объектом:
```
{
  "code": 400,
  "message": "Invalid input data provided"
}
```
