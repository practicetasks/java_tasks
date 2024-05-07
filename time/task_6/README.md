# Задача

Компания по производству часов ОАО «Счастливые» попросила вас написать серверную составляющую для их новой модели. В ней
должно быть пять кнопок:

- Меняющая временную зону на следующую по списку (список должен проходиться по кругу).
- Сдвигающая время на 10 часов вперёд.
- Сдвигающая время на 1 час вперёд.
- Сдвигающая время на 10 минут вперёд.
- Сдвигающая время на 1 минуту вперёд.

Реализуйте указанные методы и выставьте с помощью них следующее время: 18 часов, 26 минут, атырауский часовой пояс.

Ожидаемый результат:
```
2024-01-12T18:26+05:00[Asia/Atyrau]
```


```java
import java.time.LocalDateTime;
import java.time.ZoneId;
import java.time.ZonedDateTime;
import java.util.Arrays;
import java.util.List;

public class Practice {
    public static void main(String[] args) {
        Watch watch = new Watch();

        // настройка часов

        System.out.println(watch.getCurrentTime());
    }
}

class Watch {
    private ZonedDateTime currentTime;
    private int numOfZone;
    private final List<String> zones = Arrays.asList("America/New_York", "Asia/Qyzylorda", "Asia/Atyrau");

    public Watch() {
        numOfZone = 0;
        ZoneId zone = ZoneId.of(zones.get(numOfZone));
        LocalDateTime dateTime = LocalDateTime.of(2024, 1, 12, 0, 0);
        currentTime = ZonedDateTime.of(dateTime, zone);
    }

    public void changeTimeZone() {
        numOfZone = ...;
        ZoneId newZone = ZoneId.of(zones.get(numOfZone));
        // смените временную зону (время должно остаться прежним)
        ...
    }

    public void addTenHours() {
        // увеличьте текущее время на 10 часов
        ...
    }

    public void addHour() {
        // увеличьте текущее время на 1 час
        ...
    }

    public void addTenMinutes() {
        // увеличьте текущее время на 10 минут
        ...
    }

    public void addMinute() {
        // увеличьте текущее время на 1 минуту
        ...
    }

    public ZonedDateTime getCurrentTime() {
        // верните текущее время
        ...
    }
}
```
