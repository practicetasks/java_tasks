# Задача 1
Будет здорово, если финансовое приложение научится записывать ваши ежедневные расходы. Для этого нужно доработать код приложения.
1. В этой теме вы много работали с массивами трат за неделю. Добавьте в приложение пустой массив для учёта расходов за неделю с именем `expenses`.
2. Добавьте в цифровое меню приложения новую команду «3 — Ввести трату».
3. Допишите условие ветвления для обработки новой команды.
4. Внутри нового ветвления попросите пользователя выбрать день, за который он хочет внести расходы, а потом указать их сумму. Запишите траты в массив.
5. Учтите, что если в массиве уже сохранены какие-то расходы за выбранный день, то они должны суммироваться с новыми. Обратите внимание, что нумерация дней недели и нумерация индексов в массиве отличаются и вам нужно скорректировать это.

```java
import java.util.Scanner;

public class Practice {
    public static void main(String[] args) {
        // Ниже объявите пустой массив expenses для записи трат за неделю
        ...

        double rateUSD = 450;
        double rateEUR = 500;
        double rateRUB = 5;

        Scanner scanner = new Scanner(System.in);

        System.out.println("Сколько денег у вас осталось до зарплаты?");
        double moneyBeforeSalary = scanner.nextDouble();

        System.out.println("Сколько дней до зарплаты?");
        int daysBeforeSalary = scanner.nextInt();

        while (true) {
            System.out.println("Что вы хотите сделать?");
            System.out.println("1 — Конвертировать валюту");
            System.out.println("2 — Получить совет");
            ... // Допишите вывод нового пункта меню
            System.out.println("0 — Выход");

            int command = scanner.nextInt();

            if (command == 1) {
                System.out.println("Ваши сбережения: " + moneyBeforeSalary + " KZT");
                System.out.println("В какую валюту хотите конвертировать? Доступные варианты: 1 - USD, 2 - EUR, 3 - RUB.");
                int currency = scanner.nextInt();
                if (currency == 1) {
                    System.out.println("Ваши сбережения в долларах: " + moneyBeforeSalary / rateUSD);
                } else if (currency == 2) {
                    System.out.println("Ваши сбережения в евро: " + moneyBeforeSalary / rateEUR);
                } else if (currency == 3) {
                    System.out.println("Ваши сбережения в рублях: " + moneyBeforeSalary / rateRUB);
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
            } else if (command == 3) { // Ещё одно ветвление для обработки новой команды, допишите его условие
                // Допишите код для печати сообщения для пользователя
                // Текст сообщения: "За какой день вы хотите ввести трату: 1-ПН, 2-ВТ, 3-СР, 4-ЧТ, 5-ПТ, 6-СБ, 7-ВС?"
                ...
                // Получите из консоли день, за который пользователь хочет указать расходы
                int day = ...
                System.out.println("Введите размер траты:");
                // Получите из консоли значение расходов и сохраните в переменной expense
                ...
                // Сохраните полученное значение дневных трат в массив expenses
                // Не забудьте прибавить новое значение к уже существующим тратам
                ...
                System.out.println("Значение сохранено!");

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