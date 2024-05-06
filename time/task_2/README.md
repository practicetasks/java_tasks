# Задача

У индонезийской службы доставки JavaDelivery горячий сезон: она работает круглосуточно и ей срочно нужна программа для
составления графика работы курьеров. Вам необходимо реализовать метод, который будет выводить на экран график в таком
формате:

```
Расписание смен:
1 смена. Начало: 2025-06-01T08:30, конец: 2025-06-01T13:30
2 смена. Начало: 2025-06-01T13:30, конец: 2025-06-01T18:30
3 смена. Начало: 2025-06-01T18:30, конец: 2025-06-01T23:30
4 смена. Начало: 2025-06-01T23:30, конец: 2025-06-02T04:30
5 смена. Начало: 2025-06-02T04:30, конец: 2025-06-02T09:30
```

Входные данные для этого метода:
- время начала рабочей смены (часы, минуты),
- продолжительность смены в часах,
- количество смен в графике.

Для теста выбрана дата 1 июня 2025 года. Добавьте проверку на то, что продолжительность одной смены — не более 8 часов.

```java
import java.time.LocalDateTime;

import static java.time.Month.JUNE;

public class Practice {

    public static final int START_YEAR = 2025;
    public static final int START_DAY = 1;
    public static final int MAX_SHIFT = 8;

    public static void main(String[] args) {
        printWorkHours(8, 30, 5, 5);
    }

    private static void printWorkHours(
            int startHours, // час, с которого начинается рабочая смена
            int startMinutes, // минута, с которой начинается рабочая смена
            int shiftContinuation, // продолжительность смены в часах
            int shiftAmount // количество смен
    ) {
        if (...){ // продолжительность смены не должна быть больше MAX_SHIFT часов
            System.out.println("Выбрано слишком большое время для рабочей смены!");
        }
        System.out.println("Расписание смен:");
        // создайте экземпляр класса:
        // сформируйте дату и время начала первой смены.
        // год и месяц уже заданы в константах.
        LocalDateTime startTime = ...
        LocalDateTime endTime;
        for (...){ // цикл должен начинаться с 1, а количество итераций должно быть равно количеству смен
            endTime = ... // вычислите дату и время окончания смены
            System.out.println("Cмена " + i + ". Начало: " + startTime + ", конец: " + endTime);
            ... // обновите переменную startTime
        }
    }
}
```