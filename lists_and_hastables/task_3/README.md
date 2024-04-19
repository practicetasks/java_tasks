# Задача 
Теперь, когда приложение работает со списками, можно расширить его функционал.
1. Добавьте в класс `Practice` две новые команды меню:
    * «6 — Очистить список трат»;
    * «7 — Найти и удалить трату».
2. Новые команды должны обращаться к методам класса `ExpensesManager` — напишите их:
    * метод `removeAllExpenses()` должен очищать список трат и печатать фразу «Список трат пуст.».
    * метод `removeExpense(double expense)` должен проверять, содержится ли указанное пользователем значение в списке. Если в списке нет ни одной траты, то нужно сообщить пользователю, что «Список трат пуст.». Если трата найдена, то её нужно удалить и сообщить об этом. Если указанной суммы расходов в списке нет, то нужно вывести на экран, что «Такой траты нет».
    * Чтобы удалить элемент, вам потребуется вычислить его индекс — используйте для этого цикл и не забудьте его прервать. Найденный индекс сохраните в переменную `index`.


#### ExpensesManager
```java
import java.util.ArrayList;

public class ExpensesManager {
    ArrayList<Double> expenses;

    ExpensesManager() {
        expenses = new ArrayList<>();
    }

    double saveExpense(double moneyBeforeSalary, double expense) {
        moneyBeforeSalary = moneyBeforeSalary - expense;
        expenses.add(expense);
        System.out.println("Значение сохранено! Ваш текущий баланс в тенге: " + moneyBeforeSalary);
        if (moneyBeforeSalary < 5000) {
            System.out.println("На вашем счету осталось совсем немного. Стоит начать экономить!");
        }
        return moneyBeforeSalary;
    }

    void printAllExpenses() {
        for (int i = 0; i < expenses.size(); i++) {
            System.out.println("Трата № " + (i + 1) + ". Потрачено " + expenses.get(i) + " тенге");
        }
    }

    double findMaxExpense() {
        double maxExpense = 0;
        for (Double exp : expenses) {
            if (exp > maxExpense) {
                maxExpense = exp;
            }
        }
        return maxExpense;
    }
    
    // Добавьте метод removeAllExpenses()
    ... // Текст для печати: "Список трат пуст."
    
    // Добавьте метод removeExpense(double expense)
    ... /* Текст для печати: "Список трат пуст."
        "Трата удалена!"
        "Такой траты нет." */

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

        Converter converter = new Converter(444.06, 489.32, 4.88);
        DinnerAdvisor dinnerAdvisor = new DinnerAdvisor();
        ExpensesManager expensesManager = new ExpensesManager();

        while (true) {
            printMenu();
            int command = scanner.nextInt();

            if (command == 1) {
                System.out.println("Ваши сбережения: " + moneyBeforeSalary + " KZT");
                System.out.println("В какую валюту хотите конвертировать? Доступные варианты: 1 - USD, 2 - EUR, 3 - RUB.");
                int currency = scanner.nextInt();
                converter.convert(moneyBeforeSalary, currency);
            } else if (command == 2) {
                dinnerAdvisor.getAdvice(moneyBeforeSalary, daysBeforeSalary);
            } else if (command == 3) {
                System.out.println("Введите размер траты:");
                double expense = scanner.nextDouble();
                moneyBeforeSalary = expensesManager.saveExpense(moneyBeforeSalary, expense);
            } else if (command == 4) {
                expensesManager.printAllExpenses();
            } else if (command == 5) {
                System.out.println("Самая большая сумма расходов составила " + expensesManager.findMaxExpense() + " тенге.");
            } else ... { // Добавьте реализацию команды 6 
						    ... // Вызовите соответствующий метод
            } else ... { // Добавьте реализацию команды 7 
                if ... { // Проверьте наличие значений в списке
                  System.out.println("Введите трату:");
                  double expense = ...; // Считайте значение траты
                  ... // Вызовите соответствующий метод
                } else{
                  	System.out.println("Список трат пуст.");
                }
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
        // Добавьте новые пункты в меню:
        ... // "6 - Очистить список трат"
        ... // "7 - Найти и удалить трату"
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

###### Подсказки
* Методы `removeAllExpenses()` и `removeExpense(double expense)` ничего не возвращают — их тип `void`.
* Внутри `removeAllExpenses()` должен вызываться метод для очистки списка — `expenses.clear()`.
* Внутри `removeExpense(double expense)` нужно написать ветвление, где сначала проверить, если ли значения в списке — `expenses.isEmpty()`.
* Если список не пустой, то нужно проверить, есть ли в нём нужный элемент — `expenses.contains(expense)`.
* Чтобы удалить элемент, нужно вычислить его индекс с помощью полной формы цикла `for (int i = 0; i < expenses.size(); i++)`. `Если expenses.get(i) == expense`, то можно сохранить значение переменной итерирования `index = i` и прервать цикл с помощью `break`.
* Проверьте, не забыли ли вы объявить переменную `int index`. Её начальное значение равно 0.
* Удалить элемент нужно так — `expenses.remove(index)`.