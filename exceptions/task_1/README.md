# Задача


Приложения часто должны обрабатывать и преобразовывать данные, которые поступили от пользователей. Важно уметь
обрабатывать ошибки при вводе и уметь ограничивать количество попыток, в том числе и с помощью написания собственных
классов-исключений.
<br>
<br>
Перед вами программа-калькулятор сложных процентов. Допишите код классов-исключений `LimitException` (для ограничения
количества попыток) и `InputException` (для ошибок при вводе), а также добавьте их обработку.

1. Исключение `LimitException` должно быть унаследовано от класса `RuntimeException`. Помимо текста исключения оно должно
   принимать количество попыток ввода `attempts` в виде целого числа.
2. Добавьте обработку `LimitException` в методе `main()`. При превышении лимита попыток предусмотрите вывод сообщения:
   Превышен лимит ошибок ввода: `n`, где `n` — количество реальных попыток.
3. Исключение `InputException` должно быть унаследовано от класса `Exception`. При обработке ошибки предусмотрите вывод для
   пользователей следующих сообщений:

   * Введено отрицательное значение;
   * Введено не число;
   * Ошибка ввода: <подробное сообщение об ошибке>.

4. Сгенерируйте нужные исключения внутри класса `FinancialCalculatorException`.

```java
public class LimitException {
}
```

```java
public class InputException {
}
```



```java
import java.util.InputMismatchException;
import java.util.Scanner;

public class FinancialCalculatorException {
  	final static Scanner scanner = new Scanner(System.in);
    public static void main(String[] args) {
        calculate();
        // перехват исключения LimitException
    }

    public static double getInterest(final double rate, final int time, final double principal) {
        final double multiplier = Math.pow(1.0 + rate/100.0, time) - 1.0;
        return multiplier * principal;
    }

    public static int getIntLimited(String greeting, int attempts) {
        for (int counter = 0; counter < attempts; counter++) {
            try {
                System.out.println(greeting + " => ");
                try {
                    final int value = Integer.parseInt(scanner.nextLine());
                    // проверка на отрицательное значение
                    // сгенерируйте исключение "Введено отрицательное значение"
                    return value;
                } catch (NumberFormatException exception) {
                    // сгенерируйте исключение "Введено не число"
                }
            } catch (InputException exception) {
                // сгенерируйте вывод формата "Ошибка ввода: " + информация об исключении
            }
        }
        // сгенерируйте исключение LimitException с сообщением "Превышен лимит ошибок ввода"
    }

    public static double getDoubleLimited(String greeting, int attempts) {
        for (int counter = 0; counter < attempts; counter++) {
            try {
                System.out.println(greeting + " => ");
                // добавьте недостающий код
                try {
                    final double value = Double.parseDouble(scanner.nextLine());
                    // ...
                    // ...
                    return value;
                } catch (NumberFormatException exception) {
                    // ...
                }
            } catch (InputException exception) {
                // ...
            }
        }
        // сгенерируйте исключение LimitException
    }

    public static void calculate() {
        final double rate = getDoubleLimited("Введите ставку", 3);
        final double principal = getDoubleLimited("Введите размер вклада", 3);
        final int time = getIntLimited("Введите срок вклада в месяцах", 5);
        System.out.println("Ваша выгода = " + getInterest(rate, time, principal));
    }
}
```