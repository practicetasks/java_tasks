# Задача

Класс `IntegerParser` преобразует строку в целое число. Строку на вход передают пользователи, а это всегда риск
некорректного ввода данных. Исключения будут генерироваться в методе `parseInt()`.

Важно обработать все исключения так, чтобы в случае, если они произойдут, пользователи увидели сообщения, с помощью
которых могут исправить допущенную ошибку ввода.

Для каждого типа исключений должен быть настроен свой вывод.

- `EmptyStringException` — `"Введена пустая строка."`
- `StringNotNumberException` — `"Вы ввели не целое число."`
- `StringIsTooBigNumberException` — `"Введённое число слишком большое."`
- `StringIsTooSmallNumberException` — `"Введённое число слишком маленькое."`

```java
import java.util.Scanner;

public class Exceptions {
    public static void main(String[] args) {
        System.out.print("Введите целое число => ");
        Scanner scanner = new Scanner(System.in);
        final String inputValue = scanner.next();
        final int parsedValue = IntegerParser.parseInt(inputValue);
        System.out.println(parsedValue);
    }
}
```

```java
import java.math.BigInteger;

public class IntegerParser {
    public static int parseInt(String inputValue) {
        if (inputValue.trim().isEmpty()) {
            throw new EmptyStringException();
        }

        if (!inputValue.matches("-?\\d+")) {
            throw new StringNotNumberException();
        }

        BigInteger value = new BigInteger(inputValue);
        if (value.compareTo(BigInteger.valueOf(Integer.MAX_VALUE)) > 0) {
            throw new StringIsTooBigNumberException();
        }

        if (value.compareTo(BigInteger.valueOf(Integer.MIN_VALUE)) < 0) {
            throw new StringIsTooSmallNumberException();
        }

        return Integer.parseInt(inputValue);
    }
}

class EmptyStringException extends RuntimeException {
}

class StringIsTooSmallNumberException extends RuntimeException {
}

class StringIsTooBigNumberException extends RuntimeException {
}

class StringNotNumberException extends RuntimeException {
}
```

_подсказки ниже)_

<br><br><br><br><br><br><br><br><br><br><br><br>

###### подсказки

- Добавьте в код конструкцию `try — catch` для вызова метода `parseInt()`.
- Блоков catch должно быть четыре. Объедините `NullStringException` и `EmptyStringException` в один блок, так как вывод там
  одинаковый.
- Проверьте, что каждому типу исключения соответствует свой текст.
- Убедитесь, что вы не обрабатываете родительские исключения `Exception` или `Throwable`.