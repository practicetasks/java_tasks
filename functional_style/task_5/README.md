# Задача

Пришло время попрактиковаться в написании кода, работающего с неизменяемыми объектами.
В приложение магазина конфет добавляется новая сущность. Теперь конфеты можно объединять в наборы! Допишите код,
создающий на основе списка конфет набор. При этом учтите такие ограничения:

- Цена конфеты в наборе всегда на 5 тенге дешевле, чем отдельно.
- Конфеты не всех производителей можно добавлять наборы — некоторые запрещают это. Список запрещенных для наборов
  производителей задан заранее.
- Конфеты в наборе должны быть отсортированы по названию.

За набор отвечает класс `CandyBox` - он уже частично реализован. Он состоит из названия набора, списка конфет в нем и их
количества. В этом же классе в виде статического поля `prohibitedProducers` хранится список запрещенных производителей -
метод `isProducerAllowed` проверяет конфету на валидность ее производителя в соответствии с этим списком. Вам нужно
доработать класс `CandyBox`, а потом добавить в класс `CandyBoxesStore` код, который будет создавать набор конфет.
Используйте ссылки на методы, где возможно. И помните — в вашем коде не должно быть изменяемых объектов!

```java
import java.util.Collection;
import java.util.Set;

public class Candy {
    //название
    final String name;
    //производитель
    final String producer;
    //цена
    final int price;
    //проданное количество
    final int amountSold;
    //другие варианты названия
    final Set<String> alternateNames;

    public Candy(String name, String producer, int price, int amountSold, Collection<String> alternateNames) {
        this.name = name;
        this.producer = producer;
        this.price = price;
        this.amountSold = amountSold;
        this.alternateNames = Set.copyOf(alternateNames);
    }

    public static int compareByName(Candy c1, Candy c2) {
        return c1.name.compareTo(c2.name);
    }
}
```

```java
import java.util.List;

public class CandyBox {
    final String boxTitle;
    final List<Candy> candies;
    final long numberOfCandies;

    private static final List<String> prohibitedProducers = List.of("Рахат");

    //добавьте конструктор

    public static boolean isProducerAllowed(Candy candy) {
        //добаьте тело метода
    }

    public void printContent() {
        System.out.println("Набор " + boxTitle
                + ", содержит " + numberOfCandies + " конфет");
        candies.forEach(candy ->
                System.out.println(candy.name + " производства " + candy.producer + ", цена: " + candy.price));
    }
}
```

```java
import java.util.List;
import java.util.stream.Collectors;

public class CandyBoxesStore {
    public static void main(String[] args) {
        Candy candy1 = new Candy("Рахат", "Рахат", 28, 4, Set.of("Рафаэлло", "Қарақұм"));
        Candy candy2 = new Candy("Шокобар", "Баян Сұлу", 32, 2, Set.of("Шоко", "Баян"));
        Candy candy3 = new Candy("Ақ Тілегім", "Рахат", 44, 5, Set.of("Ақ тілегім", "Ақ тілек"));
        Candy candy4 = new Candy("Тайжану", "Баян Сұлу", 14, 12, Set.of("ТАЙЖАНУ"));

        List<Candy> candies = List.of(candy1, candy2, candy3, candy4);

        List<Candy> candiesForBox = //добавьте код здесь

        CandyBox candyBox = new CandyBox("С Новым Годом", candiesForBox);

        candyBox.printContent();
    }
}
```

- Создайте в `CandyBox` конструктор с двумя аргументами — именем набора и списком конфет. Количество конфет в наборе
  должно вычисляться автоматически на основе списка конфет.
- Для формирования набора используйте стрим. Отфильтруйте конфеты по производителю с использованием
  метода `isProducerAllowed`. Не забудьте создать новый экземпляр конфеты с уменьшенной ценой.
- Чтобы отсортировать конфеты по названию, можно использовать операцию стрима `sorted`. На вход она принимает
  функцию-компаратор, в качестве которой можно использовать ссылку на метод `compareByName`.