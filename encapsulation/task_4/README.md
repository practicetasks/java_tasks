
# Задача: Реализация класса Order

Создайте класс Order, который представляет заказ в интернет-магазине.


#### Поля класса (все private)
•	id (int) — идентификатор заказа
•	customerName (String) — имя клиента
•	itemsCount (int) — количество товаров
•	totalPrice (double) — сумма заказа без скидки
•	discountPercent (int) — скидка в процентах (0..30)
•	status (String) — статус заказа

⸻

#### Допустимые статусы (строки)

Использовать только следующие значения:
•	"NEW"
•	"CONFIRMED"
•	"SHIPPED"
•	"DELIVERED"
•	"CANCELLED"

⸻

### Требования

#### Инкапсуляция
•	Все поля должны быть private.
•	Доступ к данным — только через геттеры.
•	Не у всех полей должен быть сеттер.
•	Статус нельзя менять напрямую через сеттер.

⸻

#### Конструктор

Order(int id, String customerName)

При создании заказа:
•	сохранить id
•	установить имя клиента с валидацией
•	установить:
•	status = "NEW"
•	itemsCount = 0
•	totalPrice = 0.0
•	discountPercent = 0

⸻

#### Валидация

customerName

Метод setCustomerName(String name):
•	не null
•	не пустая строка после trim()

⸻

discountPercent

Метод setDiscountPercent(int discountPercent):
•	значение от 0 до 30 включительно

⸻

itemsCount и totalPrice
•	Нельзя менять напрямую через сеттеры.
•	Изменяются только через методы:
•	addItem(double price)
•	removeItem(double price)

⸻

#### Работа с товарами

➕ Метод addItem(double price)

Должен:
•	Проверять price > 0
•	Запрещать добавление, если статус:
•	"SHIPPED"
•	"DELIVERED"
•	"CANCELLED"
•	Увеличивать itemsCount
•	Увеличивать totalPrice
•	Выводить сообщение об успехе или ошибке

⸻

➖ Метод removeItem(double price)

Должен:
•	Проверять price > 0
•	Разрешать удаление только если статус:
•	"NEW" или "CONFIRMED"
•	Запрещать удаление если itemsCount == 0
•	После удаления:
•	уменьшать itemsCount
•	уменьшать totalPrice
•	Запрещать ситуацию, когда totalPrice станет меньше 0

⸻

#### Смена статусов

Статус нельзя менять напрямую.

⸻

confirm()

Можно вызвать только если статус "NEW".

⸻

ship()

Можно вызвать только если статус "CONFIRMED".

⸻

deliver()

Можно вызвать только если статус "SHIPPED".

⸻

cancel()

Можно вызвать только если статус:
•	"NEW"
•	"CONFIRMED"

⸻

#### Итоговая цена

Метод:

double getFinalPrice()

Возвращает:

totalPrice * (1 - discountPercent / 100.0)


⸻

#### Метод вывода информации

void printOrderInfo()

Должен выводить:
•	id
•	customerName
•	status
•	itemsCount
•	totalPrice
•	discountPercent
•	finalPrice

⸻

### Пример использования

public class Main {
public static void main(String[] args) {
Order order = new Order(1, "Алия");

        order.addItem(1000);
        order.addItem(500);
        order.setDiscountPercent(20);

        order.ship();      // ошибка
        order.confirm();
        order.ship();

        order.addItem(200); // ошибка

        order.printOrderInfo();

        order.cancel();    // ошибка
        order.deliver();

        order.printOrderInfo();
    }
}


⸻

#### Пример ожидаемого вывода

```
Товар добавлен: 1000.0
Товар добавлен: 500.0
Скидка установлена: 20%

Нельзя отправить заказ. Статус должен быть CONFIRMED.

Заказ подтвержден.
Заказ отправлен.

Нельзя изменить заказ после отправки.

------------------------
Заказ #1
Клиент: Алия
Статус: SHIPPED
Количество товаров: 2
Сумма без скидки: 1500.0
Скидка: 20%
Итого: 1200.0
------------------------

Нельзя отменить заказ со статусом SHIPPED.
Заказ доставлен.

------------------------
Заказ #1
Клиент: Алия
Статус: DELIVERED
Количество товаров: 2
Сумма без скидки: 1500.0
Скидка: 20%
Итого: 1200.0
------------------------
```


