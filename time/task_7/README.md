# Задача

Международный аэропорт имени Ады Лавлейс обратился к вам за помощью. Реализуйте метод, который будет выводить на информационное табло текущие дату и время в указанных городах в следующем формате:

```
Қызылорда:
07.05.2024; 16:36:41. +05:00
Осло:
07.05.2024; 13:36:41. +02:00
Чикаго:
07.05.2024; 06:36:41. -05:00
Шанхай:
07.05.2024; 19:36:41. +08:00
Аддис-Абеба:
07.05.2024; 14:36:41. +03:00
```

```java
import java.time.Instant;
import java.time.ZoneId;
import java.time.ZonedDateTime;
import java.time.format.DateTimeFormatter;

public class Practice {
    public static void main(String[] args) {
        Instant now = Instant.now();

        // укажите корректный формат вывода даты
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd.MM.yyyy; HH:mm:ss. ZZZZZ");

        // создайте экземпляр ZoneId для Кызылорды
        ZoneId qyzylordaZone = ...
        ZonedDateTime qyzylordaDateTime = ...

        printTime(formatter, qyzylordaDateTime, "Қызылорда");

        convertAndPrintTime(formatter, qyzylordaDateTime, "Осло", "Europe/Oslo");
        convertAndPrintTime(formatter, qyzylordaDateTime, "Чикаго", "America/Chicago");
        convertAndPrintTime(formatter, qyzylordaDateTime, "Шанхай", "Asia/Shanghai");
        convertAndPrintTime(formatter, qyzylordaDateTime, "Аддис-Абеба", "Africa/Addis_Ababa");
    }

    private static void convertAndPrintTime(DateTimeFormatter formatter, ZonedDateTime qyzylordaDateTime, String cityName, String region) {
        ZoneId newZone = ... // создайте ZoneId из region
        ZonedDateTime newDateTime = ... // измените временную зону у qyzylordaDateTime

        printTime(formatter, newDateTime, cityName);
    }

    private static void printTime(DateTimeFormatter formatter, ZonedDateTime dateTime, String cityName) {
        System.out.println(cityName + ":");
        // выведите dateTime в указанном в formatter формате
        System.out.println(...);
    }
}
```