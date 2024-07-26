# Задача

🔵 Сортировать конфеты требуется не только по названию, но и по цене, а отображать результаты сортировки хорошо бы в
максимально кратком формате. Такую функциональность вам предстоит добавить самостоятельно.

Реализуйте в классе `Candy` статический метод `compareByPrice` для сортировки по цене конфеты. Также вам нужно добавить
нестатический метод `printNameWithPrice`, который выводит на экран название и цену текущей конфеты в формате `«название:
цена»`.

Добавьте вызов сортировки по цене в `main`. Результаты сортировки по названию и по цене выведите на экран, используя
метод
`printNameWithPrice`.

```java
import java.util.Collection;
import java.util.Set;

public class Candy {
    final String name;
    final String producer;
    final int price;
    final int amountSold;
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

    public static int compareByPrice(Candy c1, Candy c2) {
        //вставьте код здесь
    }

    public void printNameWithPrice() {
        //вставьте код здесь
    }

    @Override
    public String toString() {
        return "Candy{" +
                "name='" + name + '\'' +
                ", producer='" + producer + '\'' +
                ", price=" + price +
                ", amountSold=" + amountSold +
                ", alternateNames=" + alternateNames +
                '}';
    }
}
```

```java
import java.util.List;
import java.util.Arrays;

public class CandyStore {
    public static void main(String[] args) {
        Candy candy1 = new Candy("Рахат", "Рахат", 28, 4, Set.of("Рафаэлло", "Қарақұм"));
        Candy candy2 = new Candy("Шокобар", "Баян Сұлу", 32, 2, Set.of("Шоко", "Баян"));
        Candy candy3 = new Candy("Ақ Тілегім", "Рахат", 44, 5, Set.of("Ақ тілегім", "Ақ тілек"));
        Candy candy4 = new Candy("Тайжану", "Баян Сұлу", 14, 12, Set.of("ТАЙЖАНУ"));

        Candy[] candies = {candy1, candy2, candy3, candy4};

        System.out.println("Сортировка по имени");
        Arrays.sort(candies, Candy::compareByName);
        Arrays.stream(candies).forEach(/* вставьте код здесь*/);

        System.out.println("Сортировка по цене");
        Arrays.sort(candies, /* вставьте код здесь*/);
        Arrays.stream(candies).forEach(/* вставьте код здесь*/);
    }
}
```

_подсказки ниже :)_

<br><br><br><br><br><br><br><br><br><br><br><br>

- Реализуйте метод `compareByPrice` по аналогии с методом `compareByName`.
- Для реализации метода `printNameWithPrice` используйте вызов `System.out.println` и передайте в него строку в нужном формате.
- Чтобы вызвать внутри `forEach` метод очередного объекта списка, используйте синтаксис `Candy::имя метода`
