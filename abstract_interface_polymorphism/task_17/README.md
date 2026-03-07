# Задача: Доставка еды

В системе есть разные способы доставки заказа из ресторана.

Все способы доставки имеют общий метод deliver(), но выполняют его по-разному.



### Базовый класс Delivery

Поля
- String orderId
- String address

Конструктор
- Принимает orderId, address.

Методы
- void deliver()
   
  Базовое поведение:
  - `Delivering order <orderId> to <address>`

String getType()
- Возвращает "Standard".

---

## Наследники

---

### CarDelivery

Доп. поле
- String driverName

Переопределить deliver():
- `Driver <driverName> is delivering order <orderId> by car to <address>`

getType() → "Car"

---

### BikeDelivery

Доп. поле
- String courierName

Переопределить deliver():
- `Courier <courierName> is delivering order <orderId> by bike to <address>`

getType() → "Bike"

--- 

### ScooterDelivery

Доп. поле
- String courierName

Переопределить deliver():
- `Courier <courierName> is delivering order <orderId> by scooter to <address>`

getType() → "Scooter"

--- 

### Что нужно сделать в main

Вам необходимо:

1. Создать ArrayList<Delivery>.
2. Добавить в список разные типы доставки:

   - `CarDelivery("#101", "Green Street 12", "Alex")`
   - `BikeDelivery("#102", "Main Avenue 5", "Timur")`
   - `ScooterDelivery("#103", "Park Road 7", "Dana")`

3. Пройтись по списку циклом for и вызвать у каждого deliver()

---

##### Ожидаемый результат

```
Driver Alex is delivering order #101 by car to Green Street 12
Courier Timur is delivering order #102 by bike to Main Avenue 5
Courier Dana is delivering order #103 by scooter to Park Road 7
```

