## Задача: Система доставки

### Базовый класс Delivery

Поля:

- String id — номер доставки
- double distanceKm — расстояние
- double weightKg — вес
- boolean fragile — хрупкий груз

Конструктор на все поля + геттеры.

Методы:

1. `double calculatePrice()`
    - базовая цена: `distanceKm * 60`
    - `weightKg * 120`
    - если `fragile == true`, + 500
    - вернуть итог

2. `String getType()` — возвращает "Delivery"
3. `void printReceipt()` Печатает:

        ID: <id>
        Type: <getType()>
        Distance: <distanceKm> km
        Weight: <weightKg> kg
        Fragile: <fragile>
        Price: <calculatePrice>


### Наследники

`CourierDelivery` (курьер)

Доп. поле:
• boolean express

Правила:
- если distanceKm > 20 → доставка невозможна, calculatePrice() возвращает -1
- если express == true → итоговая цена умножается на 1.5

Переопределить getType() → "Courier"

---

PickupDelivery (самовывоз)

Доп. поле:
• double discountPercent

Правила:
- цена = базовая цена из super.calculatePrice()
- затем скидка: price -= price * (discountPercent / 100)
- но скидка не может быть больше 30% (если больше — считать как 30)

getType() → "Pickup"

---

TruckDelivery (грузовик)

Доп. поле:
- int loaders — количество грузчиков

Правила:
- грузовик обязателен если weightKg > 30
- цена = super.calculatePrice()
  - loaders * 700
- если fragile == true и weightKg > 50 → + 1000 (усиленная упаковка)

getType() → "Truck"

---

### Main

```java
public class Main {
   public static void main(String[] args) {
        CourierDelivery courier1 =
                new CourierDelivery("A-101", 12, 3, false, true);

        CourierDelivery courier2 =
                new CourierDelivery("A-102", 25, 2, false, false);

        PickupDelivery pickup =
                new PickupDelivery("B-201", 5, 6, true, 40);

        TruckDelivery truck1 =
                new TruckDelivery("C-301", 30, 60, true, 2);

        TruckDelivery truck2 =
                new TruckDelivery("C-302", 10, 20, false, 1);


        courier1.printReceipt();
        if (courier1.calculatePrice() == -1) {
            System.out.println("Delivery A-101 is not available.");
        }
        System.out.println();

        courier2.printReceipt();
        if (courier2.calculatePrice() == -1) {
            System.out.println("Delivery A-102 is not available.");
        }
        System.out.println();

        pickup.printReceipt();
        System.out.println();

        truck1.printReceipt();
        System.out.println();

        truck2.printReceipt();
    }
}
```