# Задача

Допишите объявление класса `Printer`, который обеспечивает механизм работы принтера ценников в магазине: из разных
магазинов в него поступают цены товаров в центах, а для печати на ценниках принтер преобразует цены в доллары.

```java
import java.util.ArrayList;
import java.util.List;

public class Practice {
    public static void main(String[] args) {
        // Первый магазин продает дорогие товары и хочет передавать цент с типом Long
        List<Long> longList = new ArrayList<>();
        longList.add(Long.MAX_VALUE);

        Printer<Long> longPrinter = new Printer<>(longList);
        longPrinter.print();

        // Второй магазин продает товары подешевле и использует для передачи цент с типом Integer
        List<Integer> intList = new ArrayList<>();
        intList.add(100000);

        Printer<Integer> integerPrinter = new Printer<>(intList);
        integerPrinter.print();

        List<String> stringList = new ArrayList<>();
        stringList.add("Hello");

        // Этот вариант должен вызывать ошибку компиляции
        // Printer<String> stringPrinter = new Printer<>(stringList);
        // stringPrinter.print();
    }
}
```

```java
public class Printer... {
    private final List<...> list;

    public Printer(... list) {
        this.list = list;
    }

    public void print() {
        for (int i = 0; i < list.size(); i++) {
            double price = list.get(i).doubleValue() / 100;
            System.out.println("Цена товара: " + price + " $.");
        }
    }
}
```