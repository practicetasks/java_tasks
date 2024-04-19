# Задача 
Завершите работу над кодом финансового приложения — соберите в отдельный класс код, касающийся трат пользователя. Назовите этот класс `ExpensesManager` (англ. «менеджер по расходам») и опишите его, действуя по пунктам:
1. Объявите одно поле — массив трат `double[] expenses`.
2. Объявите конструктор без параметров, а внутри него инициализируйте массив так же, как это происходит сейчас в классе `Practice`, — в нём должно храниться семь значений.
3. Перенесите в `ExpensesManager` код методов `saveExpense`, `findMaxExpense` и `printAllExpenses`. Удалите перед названием методов слова `public` и `static`.
4. В классе `Practice` должно остаться взаимодействие с пользователем — печать меню, вопросов пользователю, а также считывание его ответов: команд, значений зарплаты, дней и трат.
5. Параметры метода `saveExpense` внутри класса `ExpensesManager` изменятся: теперь он должен принимать остаток на счёте `moneyBeforeSalary`, размер траты `expense` и номер дня недели `day`, за который нужно её учесть.
6. Уберите из методов `findMaxExpense` и `printAllExpenses` параметр `double[] expenses`. Теперь он стал полем класса, и его не нужно передавать. 
7. Создайте объект класса `ExpensesManager` и вызовите его методы внутри класса `Practice`.

```java
import java.util.Scanner;

public class Practice {
    public static void main(String[] args) {
        double[] expenses = new double[7]; // Должно стать полем нового класса

        Scanner scanner = new Scanner(System.in);
        Converter converter = new Converter(444.06, 489.32, 3.81);
        DinnerAdvisor dinnerAdvisor = new DinnerAdvisor();
        ... // Здесь создайте объект класса ExpensesManager

        System.out.println("Сколько денег у вас осталось до зарплаты?");
        double moneyBeforeSalary = scanner.nextDouble();

        System.out.println("Сколько дней до зарплаты?");
        int daysBeforeSalary = scanner.nextInt();

        while (true) {
            printMenu();
            int command = scanner.nextInt();

            if (command == 1) {
                System.out.println("Ваши сбережения: " + moneyBeforeSalary + " KZT");
                System.out.println("В какую валюту хотите конвертировать? Доступные варианты: 1 - USD, 2 - EUR, 3 - JPY.");
                int currency = scanner.nextInt();
                converter.convert(moneyBeforeSalary, currency); // Вызовите метод класса Converter
            } else if (command == 2) {
                dinnerAdvisor.getAdvice(moneyBeforeSalary, daysBeforeSalary);
            } else if (command == 3) {
                moneyBeforeSalary = saveExpense(scanner, moneyBeforeSalary, expenses);
            } else if (command == 4) {
                printAllExpenses(expenses);
            } else if (command == 5) {
                System.out.println("Самая большая сумма расходов на этой неделе составила " + findMaxExpense(expenses) + "тенге");
            } else if (command == 0) {
                System.out.println("Выход");
                break;
            } else {
                System.out.println("Извините, такой команды пока нет.");
            }
        }
    }

    // Перенесите в ExpensesManager код методов saveExpense, findMaxExpense и printAllExpenses
    public static double saveExpense(Scanner scanner, double moneyBeforeSalary, double[] expenses) {

        // Печать вопросов и считывание ответов оставьте в классе Practice
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
        return moneyBeforeSalary;
    }

    public static void printAllExpenses(double[] expenses) {
        for (int i = 0; i < expenses.length; i++) {
            System.out.println("День " + (i + 1) + ". Потрачено " + expenses[i] + " тенге");
        }
    }

    public static double findMaxExpense(double[] expenses) {
        double maxExpense = 0;
        for (int i = 0; i < expenses.length; i++) {
            if (expenses[i] > maxExpense) {
                maxExpense = expenses[i];
            }
        }
        return maxExpense;
    }

    public static void printMenu() {
        System.out.println("Что вы хотите сделать? ");
        System.out.println("1 - Конвертировать валюту");
        System.out.println("2 - Получить совет");
        System.out.println("3 - Ввести трату");
        System.out.println("4 - Показать траты за неделю");
        System.out.println("5 - Показать самую большую сумму расходов за неделю");
        System.out.println("0 - Выход");
    }
}
```