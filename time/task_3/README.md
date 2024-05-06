# Задача

Игорь придумал «Шифр Игоря» — это как [шифр Цезаря](https://ru.wikipedia.org/wiki/%D0%A8%D0%B8%D1%84%D1%80_%D0%A6%D0%B5%D0%B7%D0%B0%D1%80%D1%8F), только Игоря. И без букв. В его шифре числа кодируются с помощью даты
и времени. Игорь написал метод по декодированию, но случайно стёр его и теперь не может восстановить пароль от архива с
домашней работой. К счастью, входные данные у него сохранились. Помогите Игорю восстановить пароль от важного архива!

Инструкция по декодированию:
- Объединить экземпляр даты и экземпляр времени в экземпляр `LocalDateTime`.
- От полученного момента времени вычесть 2 месяца, 25 дней и 100 минут.
- В полученном результате перемножить порядковый номер дня в году и число часов.

```java
import java.time.LocalDate;
import java.time.LocalTime;


public class Practice {
    public static void main(String[] args) {
        LocalDate secretDate = LocalDate.of(2020, 1, 10);
        LocalTime secretTime = LocalTime.of(12, 30);

        int result = decode(secretDate, secretTime);
        System.out.println(result);
    }

    private static int decode(LocalDate secretDate, LocalTime secretTime) {
        // объедините secretDate и secretTime
        ... newTime = ...

        // вычтите 2 месяца, 25 дней и 100 минут
        ... secretMoment = ...
        // найдите произведение порядкового номера дня в году и часов из secretMoment 
        return ... * ...;
    }
} 
```