**Задача:**

Создайте класс `Car`, который представляет автомобиль с полями `make` (марка), `model` (модель), `year` (год выпуска) и
`speed` (текущая скорость). Вам необходимо:

1. **Сделать поля класса приватными.**
2. **Создать методы доступа (геттеры) и модификаторы (сеттеры) для полей `make`, `model` и `year`.**
3. **Для поля `speed` создать только геттер, чтобы его нельзя было установить напрямую извне.**
4. **Добавить методы:**
    - `accelerate(int increment)`, который увеличивает скорость на заданное значение.
    - `brake(int decrement)`, который уменьшает скорость на заданное значение, не позволяя скорости стать отрицательной.

**Задание:**

- Реализуйте класс `Car` с использованием принципа инкапсуляции.

**Пример использования:**

```java
public class Main {
    public static void main(String[] args) {
        // Создаем объект класса Car
        Car car = new Car("Toyota", "Camry", 2020);

        // Выводим информацию об автомобиле
        car.printCarInfo();

        // Ускоряем автомобиль
        car.accelerate(50);
        car.printCarInfo();

        // Тормозим автомобиль
        car.brake(20);
        car.printCarInfo();

        // Пытаемся установить некорректные значения
        car.setYear(1800);   // Некорректный год выпуска
        car.setMake("");     // Пустая марка
        car.accelerate(-10); // Некорректное ускорение
        car.brake(-5);       // Некорректное торможение

        // Выводим информацию после попытки изменить данные
        car.printCarInfo();

        // Устанавливаем корректные значения
        car.setYear(2018);
        car.setMake("Honda");
        car.setModel("Accord");

        // Выводим обновленную информацию
        car.printCarInfo();
    }
}
```

**Ожидаемый результат**
```
Марка: Toyota
Модель: Camry
Год выпуска: 2020
Текущая скорость: 0 км/ч

Автомобиль ускорился на 50 км/ч.

Марка: Toyota
Модель: Camry
Год выпуска: 2020
Текущая скорость: 50 км/ч

Автомобиль замедлился на 20 км/ч.

Марка: Toyota
Модель: Camry
Год выпуска: 2020
Текущая скорость: 30 км/ч

Некорректный год выпуска.

Марка не может быть пустой.

Значение ускорения должно быть положительным.

Значение замедления должно быть положительным.

Марка: Toyota
Модель: Camry
Год выпуска: 2020
Текущая скорость: 30 км/ч

Марка: Honda
Модель: Accord
Год выпуска: 2018
Текущая скорость: 30 км/ч
```