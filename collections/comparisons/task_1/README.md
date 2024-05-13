# Задача

В приложении по прокату фильмов обнаружилась уязвимость! Для класса, представляющего дату проката фильма `DateTime`,
неправильно реализован интерфейс `Comparator<T>`. Из-за этого любой зритель может брать фильм в прокат на целый год.

Измените имплементацию интерфейса `Comparator<DateTime>` — `DateTimeComparator` таким образом, чтобы она сравнивала две даты
по всем полям, а не только по году. Взятый в прокат фильм представлен классом `RentedFilm`. Запустите код класса
`Practice`, чтобы проверить корректность вашей реализации компаратора.

```java
public class DateTime {
    public final int day;
    public final int month;
    public final int year;

    public final int hours;
    public final int minutes;
    public final int seconds;

    public DateTime(int day, int month, int year, int hours, int minutes, int seconds) {
        this.day = day;
        this.month = month;
        this.year = year;
        this.seconds = seconds;
        this.minutes = minutes;
        this.hours = hours;
    }

    @Override
    public String toString() {
        return "DateTime{" +
            "day=" + day +
            ", month=" + month +
            ", year=" + year +
            ", hours=" + hours +
            ", minutes=" + minutes +
            ", seconds=" + seconds +
            '}';
    }
}
```

```java
public class RentedFilm {
    private final String name;
    private final DateTime timeOfRent;
    private final DateTime timeOfReturn;

    public RentedFilm(String name, DateTime timeOfRent, DateTime timeOfReturn) {
        this.name = name;
        this.timeOfRent = timeOfRent;
        this.timeOfReturn = timeOfReturn;
    }

    public String getName() {
        return name;
    }

    public DateTime getTimeOfRent() {
        return timeOfRent;
    }

    public DateTime getTimeOfReturn() {
        return timeOfReturn;
    }
}
```


```java
import java.util.Comparator;

public class DateTimeComparator implements Comparator<DateTime> {

    @Override
    public int compare(DateTime dt1, DateTime dt2) {
        return Integer.compare(dt1.year, dt2.year);
    }
}
```

```java
public class Practice {
    public static void main(String[] args) {
        RentedFilm film1 = new RentedFilm(
            "Терминатор",
            new DateTime(20, 11, 2021, 10, 0, 0),
            new DateTime(27, 11, 2021, 23, 58, 58)
        );
        System.out.println("Фильм Терминатор взят в аренду: " + film1.getTimeOfRent());
        System.out.println("Фильм должен быть вернут до: " + film1.getTimeOfReturn());


        DateTime today = new DateTime(27, 11, 2021, 23, 58, 59);

        System.out.println("Сегодняшнее число: " + today);

        DateTimeComparator comparator = new DateTimeComparator();
        boolean shouldAlreadyBeReturned = comparator.compare(today, film1.getTimeOfReturn()) > 0;

        System.out.println("Прошло ли время возврата? " + (shouldAlreadyBeReturned ? "Да!" : "Нет!"));
    }
}
```

<br><br><br><br><br><br><br>

- Сравнение нужно провести по всем параметрам даты (год, месяц, день) и времени (час, минута, секунда).
- Как только найден параметр, по которому есть расхождение — необходимо вернуть результат `Integer.compare(..., ...)` в качестве результата компаратора.