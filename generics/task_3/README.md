## Универсальный магазин одежды с усложнениями:


#### Сортировка товаров:

* Добавьте в класс `Clothing` поле `comparableField`, которое может принимать значения `price`, `name` или другие критерии сортировки.
* Реализуйте интерфейс `Comparable<T>` в классе `Clothing` с использованием поля `comparableField`.
* Добавьте метод `sortItems(Comparator<T> comparator)` в класс `ShoppingCart`, который сортирует товары в корзине.

#### Система скидок:

* Создайте интерфейс `Discount` с методами `getDiscount(Clothing item)` и `getDescription()`.
* Реализуйте классы `PercentageDiscount`, `FixedDiscount` и `BuyXGetYDiscount` для разных типов скидок.
* Добавьте поле `List<Discount>` в класс `Clothing`.
* В методе `calculateTotal` класса `ShoppingCart` учитывайте скидки для каждого товара.

