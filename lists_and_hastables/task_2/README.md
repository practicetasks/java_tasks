# Задача
Перед вами код финансового приложения. Для хранения трат в 
приложении сейчас используется массив и это не очень удобно. Вам нужно провести рефакторинг с учётом новых знаний — 
сделайте так, чтобы траты хранились в списке вместо массива. 

* Внесите правки в класс `ExpensesManager` — импортируйте `ArrayList` и создайте список `expenses`.
* Поправьте код методов. Измените `saveExpense()` так, чтобы не нужно было указывать день и записываемые траты сохранялись
в списке подряд, друг за другом. В методе `findMaxExpense()` используйте сокращённую форму цикла `for`.
* Поправьте код в `Practice`. В текст меню мы уже внесли изменения. Вам осталось только удалить вопрос о выборе дня и 
* отредактировать вызов метода `saveExpense()`.


#### Converter
```java
public class Converter {
    double rateUSD;
    double rateEUR;
    double rateJPY;

    Converter(double usd, double eur, double jpy) {
        rateUSD = usd;
        rateEUR = eur;
        rateJPY = jpy;
    }

    void convert(double tenges, int currency) {
        if (currency == 1) {
            System.out.println("Ваши сбережения в долларах: " + tenges / rateUSD);
        } else if (currency == 2) {
            System.out.println("Ваши сбережения в евро: " + tenges / rateEUR);
        } else if (currency == 3) {
            System.out.println("Ваши сбережения в иенах: " + tenges / rateJPY);
        } else {
            System.out.println("Неизвестная валюта");
        }
    }
}
```


#### DinnerAdvisor
```java
public class DinnerAdvisor {
    void getAdvice(double moneyBeforeSalary, int daysBeforeSalary) {
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
    }
}
```


#### ExpensesManager
```java
... // Импортируйте ArrayList

public class ExpensesManager {
    double[] expenses; // Замените массив списком

    ExpensesManager() {
        expenses = new double[7]; // Создайте список в конструкторе
    }
    
    // Номер дня больше не нужен
    double saveExpense(double moneyBeforeSalary, double expense, int day) { 
        moneyBeforeSalary = moneyBeforeSalary - expense;
        expenses[day - 1] = expenses[day - 1] + expense; // Эту строку нужно убрать
        System.out.println("Значение сохранено! Ваш текущий баланс в тенге: " + moneyBeforeSalary);
        if (moneyBeforeSalary < 5000) {
            System.out.println("На вашем счету осталось совсем немного. Стоит начать экономить!");
        }
        return moneyBeforeSalary;
    }

    void printAllExpenses() {
        for (int i = 0; i < expenses.length; i++) {
            System.out.println("Трата № " + (i + 1) + ". Потрачено " + expenses[i] + " тенге");
        }
    }

    double findMaxExpense() {
        double maxExpense = 0;
        for (int i = 0; i < expenses.length; i++) { // Используйте сокращённую форму цикла
            if (expenses[i] > maxExpense) {
                maxExpense = expenses[i];
            }
        }
        return maxExpense;
    }
}
```


#### main
```java
import java.util.Scanner;

public class Practice {
    public static void main(String[] args) {
        
        Scanner scanner = new Scanner(System.in);
        System.out.println("Сколько денег у вас осталось до зарплаты?");
        double moneyBeforeSalary = scanner.nextDouble();
        System.out.println("Сколько дней до зарплаты?");
        int daysBeforeSalary = scanner.nextInt();

        Converter converter = new Converter(444.06, 489.32, 3.14);
        DinnerAdvisor dinnerAdvisor = new DinnerAdvisor();
        ExpensesManager expensesManager = new ExpensesManager();

        while (true) {
            printMenu();
            int command = scanner.nextInt();

            if (command == 1) {
                System.out.println("Ваши сбережения: " + moneyBeforeSalary + " KZT");
                System.out.println("В какую валюту хотите конвертировать? Доступные варианты: 1 - USD, 2 - EUR, 3 - JPY.");
                int currency = scanner.nextInt();
                converter.convert(moneyBeforeSalary, currency);
            } else if (command == 2) {
                dinnerAdvisor.getAdvice(moneyBeforeSalary, daysBeforeSalary);
            } else if (command == 3) {
                // Номер дня больше не нужен. Уберите вопрос и считывание номера дня
                System.out.println("За какой день вы хотите ввести трату: 1-ПН, 2-ВТ, 3-СР, 4-ЧТ, 5-ПТ, 6-СБ, 7-ВС?");
                int day = scanner.nextInt();
                System.out.println("Введите размер траты:");
                double expense = scanner.nextDouble();
                // Сигнатура метода изменится, учитывайте это
                moneyBeforeSalary = expensesManager.saveExpense(moneyBeforeSalary, expense, day);
            } else if (command == 4) {
                expensesManager.printAllExpenses();
            } else if (command == 5) {
                System.out.println("Самая большая сумма расходов составила " + expensesManager.findMaxExpense() + " тенге.");
            } else if (command == 0) {
                System.out.println("Выход");
                break;
            } else {
                System.out.println("Извините, такой команды пока нет.");
            }
        }
    }

    public static void printMenu() {
        System.out.println("Что вы хотите сделать? ");
        System.out.println("1 - Конвертировать валюту");
        System.out.println("2 - Получить совет");
        System.out.println("3 - Ввести трату");
        System.out.println("4 - Показать траты");
        System.out.println("5 - Показать самую большую сумму расходов");
        System.out.println("0 - Выход");
    }
}
```



<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>


###### Подсказки
* В `ExpensesManager` нужно объявить список расходов `ArrayList<Double> expenses` и создать его объект в конструкторе `expenses = new ArrayList<>()`.
* В методе `saveExpense()` не нужен номер дня — из сигнатуры нужно убрать `int day` и строку `expenses[day - 1] = expenses[day - 1] + expense`.
* При вызове `saveExpense()` в `Practice` не забудьте про обновлённую сигнатуру — `expensesManager.saveExpense(moneyBeforeSalary, expense)`.
* Введённую пользователем трату нужно сохранить в список — `expenses.add(expense)`.
* В методе `printAllExpenses()` нужно использовать вместо свойства `length` метод `size()`.
* И замените сохранения траты по номеру дня на добавление траты в список.
* Получить трату для печати нужно так — `expenses.get(i)`.
* В методе `findMaxExpense()` условие цикла будет таким `Double exp : expenses`, а условие ветвления внутри цикла таким — `exp > maxExpense`.
