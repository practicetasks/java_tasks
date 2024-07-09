# Задача

Программа по преобразованию строки в целое число немного изменилась. Теперь при исключении в блоках `catch` происходит
вызов метода `printException()`. Сейчас этот метод работает неправильно — вам нужно доработать его реализацию.

- Во-первых, `printException()` должен принимать не только сообщение об ошибке, но и само исключение.
- Во-вторых, нужно сделать так, чтобы помимо основного сообщения он выводил информацию об ошибке.
- Если у исключения есть короткое описание, то нужно вывести его, если нет, то полный стек-трейс ошибки.

```java
import java.util.Scanner;

public class StackTraceExceptions {
    public static void main(String[] args) {
        System.out.print("Введите целое число => ");
        Scanner scanner = new Scanner(System.in);
        final String inputValue = scanner.next();
        try {
            final int parsedValue = IntegerParser.parseInt(inputValue);
            System.out.println(parsedValue);
        } catch (EmptyStringException exception) {
            printException("Введена пустая строка.", exception);
        } catch (StringNotNumberException exception) {
            printException("Вы ввели не целое число.", exception);
        } catch (StringIsTooBigNumberException exception) {
            printException("Введённое число слишком большое.", exception);
        } catch (StringIsTooSmallNumberException exception) {
            printException("Введённое число слишком маленькое.", exception);
        }
    }

    private static void printException(final String message) {
        System.out.println(message);
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

<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>

- У `printException()` должно быть два параметра `final String message` и `final Throwable throwable`.
- Для получения короткого описания ошибки используйте метод `getMessage()`.
- Для вывода полного стек-трейса нужен метод `printStackTrace()`.
- Проверить, есть ли короткое описание ошибки, можно с помощью условия `if (....  != null)`.