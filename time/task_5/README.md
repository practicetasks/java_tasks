# Задача

Для космических перелётов в 2099 году используются прыжки сквозь гиперпространство. Бортовому компьютеру необходимо
знать: или прыжок будет коротким (меньше суток), и тогда продолжительность прыжка нужно выводить в минутах, или долгим,
и тогда его продолжительность нужно выводить в днях.

Для вывода временных меток используйте паттерн `"dd.MM.yyyy, HH:mm"`. Итоговый ответ должен выглядеть так:
```
Вход в гиперпространство:
10.10.2099, 12:05
Выход из гиперпространства:
10.10.2099, 14:15
Минут на гиперпрыжок: 130

Вход в гиперпространство:
10.10.2099, 12:00
Выход из гиперпространства:
11.10.2099, 15:30
Дней на гиперпрыжок: 1

Вход в гиперпространство:
10.10.2099, 23:10
Выход из гиперпространства:
11.10.2099, 10:25
Минут на гиперпрыжок: 675
```

```java
import java.time.Duration;
import java.time.LocalDateTime;
import java.time.Period;
import java.time.format.DateTimeFormatter;


public class Practice {
    public static final int SECONDS_IN_DAY = 60 * 60 * 24;

    public static void main(String[] args) {
        LocalDateTime firstStart = LocalDateTime.of(2099, 10, 10, 12, 5);
        LocalDateTime firstFinish = LocalDateTime.of(2099, 10, 10, 14, 15);

        LocalDateTime secondStart = LocalDateTime.of(2099, 10, 10, 12, 0);
        LocalDateTime secondFinish = LocalDateTime.of(2099, 10, 11, 15, 30);

        LocalDateTime thirdStart = LocalDateTime.of(2099, 10, 10, 23, 10);
        LocalDateTime thirdFinish = LocalDateTime.of(2099, 10, 11, 10, 25);


        printGap(firstStart, firstFinish);
        printGap(secondStart, secondFinish);
        printGap(thirdStart, thirdFinish);
    }

    private static void printGap(LocalDateTime start, LocalDateTime finish) {
        // используйте паттерн "dd.MM.yyyy, HH:mm"
        DateTimeFormatter formatter = ...;

        System.out.println("Вход в гиперпространство:");
        // вывод должен быть в корректном формате
        System.out.println(...);
        System.out.println("Выход из гиперпространства:");
        // вывод должен быть в корректном формате
        System.out.println(...);
        // найдите продолжительность
        Duration duration = ...;

        // сравните продолжительность в секундах с количеством секунд в сутках
        // воспользуйтесь константой SECONDS_IN_DAY
        if (...) {
            // выведите продолжительность в днях
            System.out.println("Дней на гиперпрыжок: " + ...);
        } else {
            // выведите продолжительность в минутах
            System.out.println("Минут на гиперпрыжок: " + ...);
        }
        System.out.println();
    }
}
```