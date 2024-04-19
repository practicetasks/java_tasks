# Задача с константами

Во всех банковских приложениях есть возможность перевода денег. Как правило, прежде чем выполнить перевод, система должна проверить, правильно ли введены все необходимые данные. 

<br>

Ваша задача — реализовать класс `TransactionValidator`, в котором будет находиться логика проверки суммы перевода. Минимальная сумма перевода — `MIN_AMOUNT` (100 тг.), максимальная сумма перевода — `MAX_AMOUNT` (100 000 тг.).


#### TransactionValidator
```java
public class TransactionValidator {
    // объявите константы

    // объявите метод isValidAmount()
    // внутри метода добавьте проверки на минимальную и максимальную сумму перевода
    System.out.println("Минимальная сумма перевода: " + ... + " тг. Попробуйте ещё раз!");
    System.out.println("Максимальная сумма перевода: " + ... + " тг. Попробуйте ещё раз!");
}
```

#### main
```java
import java.util.Scanner;

public class Practice {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Пожалуйста, введите сумму перевода в тенге.");
        // считайте сумму перевода

        boolean isValid = ... // добавьте вызов метод isValidAmount
        if (isValid) 
            System.out.println("Спасибо! Ваш перевод на сумму " + amount + " тг. успешно выполнен.");
        }
    }
}
```


