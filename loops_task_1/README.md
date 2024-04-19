# Задача

Вам нужно улучшить работу финансового приложения, чтобы оно стало удобным для пользователя.
* Создайте цифровое меню для выбора валют при конвертации, где 1 — `USD`, 2 — `EUR`, 3 — `JPY`.
* Добавьте в код приложения бесконечный цикл `while` и предусмотрите выход из него при выборе пользователем команды `0`.
```java
import java.util.Scanner;

public class Practice {
    public static void main(String[] args) {
        double rateUSD = 450;
        double rateEUR = 500;
        double rateJPY = 3.14;

        Scanner scanner = new Scanner(System.in);

        System.out.println("Сколько денег у вас осталось до зарплаты?");
        double moneyBeforeSalary = scanner.nextDouble();

        System.out.println("Сколько дней до зарплаты?");
        int daysBeforeSalary = scanner.nextInt();

        ...//настройте бесконечный цикл здесь
            System.out.println("Что вы хотите сделать? ");
            System.out.println("1 - Конвертировать валюту");
            System.out.println("2 - Получить совет");
            System.out.println("0 - Выход"); // Новый пункт меню, осталось только реализовать логику

            int command = scanner.nextInt();

            if (command == 1) {
                System.out.println("В какую валюту хотите конвертировать? Доступные варианты: 1 - USD, 2 - EUR или 3 - JPY.");
                int currency = ...;

                if (...) {
                    System.out.println("Ваши сбережения в долларах: " + moneyBeforeSalary / rateUSD);
                } else if (...) {
                    System.out.println("Ваши сбережения в евро: " + moneyBeforeSalary / rateEUR);
                } else if (...) {
                    System.out.println("Ваши сбережения в йенах: " + moneyBeforeSalary / rateJPY);
                } else {
                    System.out.println("Валюта не поддерживается.");
                }

            } else if (command == 2) {
                if (moneyBeforeSalary < 15_000) {
                    System.out.println("Сегодня лучше поесть дома. Экономьте и вы дотянете до зарплаты!");
                } else if (moneyBeforeSalary < 50_000) {
                    if (daysBeforeSalary < 10) {
                        System.out.println("Окей, пора в Макдак!");
                    } else {
                        System.out.println("Сегодня лучше поесть дома. Экономьте и вы дотянете до зарплаты!");
                    }
                } else if (moneyBeforeSalary < 150_000) {
                    if (daysBeforeSalary < 10) {
                        System.out.println("Неплохо! Прикупите долларов и зайдите поужинать в классное место. :)");
                    } else {
                        System.out.println("Окей, пора в Макдак!");
                    }
                } else {
                    if (daysBeforeSalary < 10) {
                        System.out.println("Отлично! Заказывайте крабов!");
                    } else {
                        System.out.println("Неплохо! Прикупите долларов и зайдите поужинать в классное место. :)");
                    }
                }
            } else if (...) {
                System.out.println("Выход");
                ...
            } else {
                System.out.println("Извините, такой команды пока нет.");
            }
        ...
    }
}
```