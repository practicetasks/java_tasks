# Задача

Представьте, что вы работаете в крупной компании над программой для учёта всей входящей корреспонденции. В эту систему
попадает информация о каждом письме, которое поступает в компанию. Письма хранятся в порядке занесения информации о них
в систему. Вам нужно добавить новую функцию `printOrderedByDateReceived` — возможность отсортировать письма по дате их
получения (от ранних к поздним). Используйте тот же формат вывода на консоль, что уже используется в программе.

```java
import java.time.LocalDate;
import java.util.LinkedHashSet;
import java.util.Set;

public class Practice {
    private static Set<Letter> letters = new LinkedHashSet<>();

    public static void main(String[] args) {
        // информация о письмах (в порядке занесения в систему)
        letters.add(new Letter("Джон Смит", LocalDate.of(2021, 7, 7), "текст письма №1 ..."));
        letters.add(new Letter("Аманда Линс", LocalDate.of(2021, 6, 17), "текст письма №2 ..."));
        letters.add(new Letter("Джо Кью", LocalDate.of(2021, 7, 5), "текст письма №3 ..."));
        letters.add(new Letter("Мишель Фернандес", LocalDate.of(2021, 8, 23), "текст письма №4 ..."));

        printOrderedById(letters);
        printOrderedByDateReceived(letters);
    }

    private static void printOrderedById(Set<Letter> letters) {
        System.out.println("Все письма с сортировкой по ID: ");

        for (Letter letter : letters) {
            System.out.println("    * Письмо от " + letter.authorName + " поступило " + letter.dateReceived);
        }
    }

    private static void printOrderedByDateReceived(Set<Letter> letters) {
        System.out.println("Все письма с сортировкой по дате получения: ");

        // реализуйте этот метод
        ...
    }
}
```

```java
public class Letter {
    public String authorName;      // имя отправителя
    public LocalDate dateReceived; // дата получения письма
    public String text;            // текст письма

    public Letter(String senderName, LocalDate dateReceived, String text) {
        this.authorName = senderName;
        this.dateReceived = dateReceived;
        this.text = text;
    }
}
```
