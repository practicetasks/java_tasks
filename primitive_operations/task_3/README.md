# Задача
В прошлой теме вы написали фрагмент кода приложения для планирования путешествия из Астаны в Париж. 
<br>
Доработайте его с учётом новых инструкций.
* Номер месяца должен быть в диапазоне от 1 до 12.
* В Астане рекомендуется остаться не только в летние, но и в зимние месяцы.
* Сравнение стоимости билетов и проверку наличия визы нужно сохранить в отдельные булевы переменные.
* Проверить наличие дешёвых билетов и визы в ветвлении нужно одним условием.

```java
import java.util.Scanner;

public class Practice {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int monthNumber;

        while (true) {
            System.out.println("Когда планируется путешествие? Введите номер месяца от 1 до 12.");
            monthNumber = scanner.nextInt();

            if (...) { // Номер месяца должен быть в диапазоне от 1 до 12
                break;
            } else {
                System.out.println("Некорретный номер месяца. Введите ещё раз.");
            }
        }

        String season = getSeasonByNumber(monthNumber);

        if (...) { // Не рекомендуем лететь в Париж в летние и зимние месяцы
            System.out.println("В это время года лучше остаться в Астане.");
            return;
        }


        System.out.println("Укажите стоимость прямых билетов из Астаны в Париж:");
        int ticketAstanaParis = scanner.nextInt();
        System.out.println("Укажите стоимость билетов из Астаны в Париж с пересадкой в Лондоне:");
        int ticketAstanaLondonParis = scanner.nextInt();
        System.out.println("У вас есть британская виза?");
        System.out.println("1 - да, виза есть");
        System.out.println("0 - визы нет");
        int britainVisa = scanner.nextInt();

        boolean directTicketsCheaper = ... // Сравнение стоимости билетов
        boolean hasBritainVisa = ... // Проверка наличия визы

        if (...) { // Проверить в одном условии наличие дешёвых билетов и визы
            System.out.println("Летим через Лондон!");
        } else {
            System.out.println("Летим через Париж!");
        }
    }

    private static String getSeasonByNumber(int monthNumber) {
        if (monthNumber < 3) {
            return "Зима";
        } else if (monthNumber < 6) {
            return "Весна";
        } else if (monthNumber < 9) {
            return "Лето";
        } else if (monthNumber < 12) {
            return "Осень";
        } else {
            return "Зима";
        }
    }
}
```