# Задача 3
Финансовое приложение теперь умеет записывать траты и выводить предупреждение о недостатке средств на счету. Однако узнать, сколько денег вы в итоге потратили в каждый из дней, не получится. Это неудобно. Доработайте функционал приложения таким образом, чтобы можно было легко получить список всех расходов за неделю с разбивкой по дням.
1. Добавьте в приложение новую команду «4 - Показать траты за неделю».
2. Напишите новое ветвление для обработки четвёртой команды. Получив её, программа должна выводить все траты за неделю в формате День _. Потрачено _ тенге.. Нумерация дней должна быть от 1 до 7.
3. Для печати трат используйте цикл `for`.

```java
import java.util.Scanner;

public class Practice {
    public static void main(String[] args) {
        double[] expenses = new double[7];

        double rateUSD = 450;
        double rateEUR = 500;
        double rateJPY = 3.14;

        Scanner scanner = new Scanner(System.in);

        System.out.println("Сколько денег у вас осталось до зарплаты?");
        double moneyBeforeSalary = scanner.nextDouble();

        System.out.println("Сколько дней до зарплаты?");
        int daysBeforeSalary = scanner.nextInt();

        while (true) {
            System.out.println("Что вы хотите сделать?");
            System.out.println("1 — Конвертировать валюту");
            System.out.println("2 — Получить совет");
            System.out.println("3 — Ввести трату");
            // Допишите новый пункт цифрового меню
            ...
            System.out.println("0 — Выход");

            int command = scanner.nextInt();

            if (command == 1) {
                System.out.println("Ваши сбережения: " + moneyBeforeSalary + " KZT");
                System.out.println("В какую валюту хотите конвертировать? Доступные варианты: 1 - USD, 2 - EUR, 3 - JPY.");
                int currency = scanner.nextInt();
                if (currency == 1) {
                    System.out.println("Ваши сбережения в долларах: " + moneyBeforeSalary / rateUSD);
                } else if (currency == 2) {
                    System.out.println("Ваши сбережения в евро: " + moneyBeforeSalary / rateEUR);
                } else if (currency == 3) {
                    System.out.println("Ваши сбережения в иенах: " + moneyBeforeSalary / rateJPY);
                } else {
                    System.out.println("Неизвестная валюта");
                }
            } else if (command == 2) {
                if (moneyBeforeSalary < 15_000) {
                    System.out.println("Сегодня лучше поесть дома. Экономьте, и вы дотянете до зарплаты!");
                } else if (moneyBeforeSalary < 50_000) {
                    if (daysBeforeSalary < 10) {
                        System.out.println("Окей, пора в Макдак!");
                    } else {
                        System.out.println("Сегодня лучше поесть дома. Экономьте, и вы дотянете до зарплаты!");
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
            } else if (command == 3) {
                System.out.println("За какой день вы хотите ввести трату: 1-ПН, 2-ВТ, 3-СР, 4-ЧТ, 5-ПТ, 6-СБ, 7-ВС?");
                int day = scanner.nextInt();
                System.out.println("Введите размер траты:");
                double expense = scanner.nextDouble();
                moneyBeforeSalary = moneyBeforeSalary - expense;
                expenses[day - 1] = expenses[day - 1] + expense;
                System.out.println("Значение сохранено! Ваш текущий баланс в тенге: " + moneyBeforeSalary);
                if (moneyBeforeSalary < 5000) {
                    System.out.println("На вашем счету осталось совсем немного. Стоит начать экономить!");
                }
              ... // Добавьте ветвление для обработки новой команды
              ... // Используйте цикл for, чтобы получить все траты — элементы массива expenses
                // Напечатайте в цикле строку: "День _. Потрачено _ тенге.".
            } else if (command == 0) {
                System.out.println("Выход");
                break;
            } else {
                System.out.println("Извините, такой команды пока нет.");
            }
        }
    }
}
```