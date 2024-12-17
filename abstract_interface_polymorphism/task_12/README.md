# Задача

Универсальный счетчик элементов

Создай класс `ElementCounter`, который позволяет подсчитывать количество вхождений элементов в коллекции любого типа
данных.

Функции класса:

1. Добавить элемент в счетчик.
2. Получить количество вхождений определенного элемента.
3. Получить общее количество элементов в счетчике.

Класс должен использовать дженерики и работать для любых типов данных.

Пример использования:
```java
public class Main {
    public static void main(String[] args) {
        // Счетчик для строк
        ElementCounter<String> stringCounter = new ElementCounter<>();
        stringCounter.add("apple");
        stringCounter.add("banana");
        stringCounter.add("apple");

        System.out.println("Количество 'apple': " + stringCounter.getCount("apple")); // 2
        System.out.println("Количество 'banana': " + stringCounter.getCount("banana")); // 1
        System.out.println("Общее количество элементов: " + stringCounter.getTotalCount()); // 3

        // Счетчик для чисел
        ElementCounter<Integer> integerCounter = new ElementCounter<>();
        integerCounter.add(1);
        integerCounter.add(2);
        integerCounter.add(1);
        integerCounter.add(3);

        System.out.println("Количество 1: " + integerCounter.getCount(1)); // 2
        System.out.println("Количество 3: " + integerCounter.getCount(3)); // 1
        System.out.println("Общее количество элементов: " + integerCounter.getTotalCount()); // 4
    }

}
```

Ожидаемый вывод:
```
Количество 'apple': 2
Количество 'banana': 1
Общее количество элементов: 3
Количество 1: 2
Количество 3: 1
Общее количество элементов: 4
```