# Задача

Доработайте код приложения для хранения и обработки паролей пользователей.

1. По аналогии с классом `ValidatePasswordException` для ошибок при вводе пароля допишите код
   класса `ValidateNameException`
   для ошибок при вводе имени пользователя. Оба класса должны наследовать от `ValidateException` и принимать короткое
   сообщение об ошибке.
2. В методах класса `PasswordMemoryStorage` пропущены предупреждения об исключении `IOException` — добавьте их.
3. Допишите код класса `NameValidator` — он должен реализовывать интерфейс `Validator` и проверять, не передана ли
   пустая
   строка. В обратном случае — генерировать исключение `ValidateNameException` с сообщением «Имя не должно быть пустым».
4. Добавьте реализованный экземпляр класса `NameValidator` в список `nameValidators`.
5. Добавьте отлов исключений `ValidateNameException` и `ValidatePasswordException` в методы класса `Practice`. При этом
   выведите сообщения формата:
    * Ошибка валидации имени: + короткое описание ошибки.
    * Ошибка валидации пароля: + короткое описание ошибки.
6. Организуйте закрытие хранилища `storage` при помощи метода `close()` при любом развитии событий в методах `addUser()`
   и
   `showUserPassword()` класса `Practice`.

#### package exceptions

```java
package exceptions;

public class ValidateException extends Exception {
    public ValidateException(final String message) {
        super(message);
    }
}
```

```java
package exceptions;

public class ValidatePasswordException extends ValidateException {
    public ValidatePasswordException(final String message) {
        super(message);
    }
}
```

```java
package exceptions;

public class ValidateNameException {
    // допишите код класса
}
```

#### package storage

```java
package storage;

import java.io.IOException;

public interface PasswordStorage {
    void open() throws IOException;

    void store(String user, String password) throws IOException;

    String get(String user) throws IOException;

    void close();
}
```

```java
package storage;

import java.io.IOException;
import java.util.HashMap;
import java.util.Map;
import java.util.Random;

public class PasswordMemoryStorage implements PasswordStorage {
    private static final Map<String, String> passwords = new HashMap<>();
    private boolean wasOpened = false;

    private boolean shouldErrorBeGenerated() {
        Random random = new Random();
        return random.nextInt(100) == 0;
    }

    @Override
    public void open() {
        if (shouldErrorBeGenerated()) {
            throw new IOException("Произошла внезапная ошибка");
        }
        wasOpened = true;
    }

    @Override
    public void store(final String user, final String password) {
        if (!wasOpened) {
            throw new IOException("Хранилище не открыто");
        }
        if (shouldErrorBeGenerated()) {
            throw new IOException("Произошла внезапная ошибка");
        }
        passwords.put(user, password);
    }

    @Override
    public String get(final String user) {
        if (!wasOpened) {
            throw new IOException("Хранилище не открыто");
        }
        if (shouldErrorBeGenerated()) {
            throw new IOException("Произошла внезапная ошибка");
        }
        return passwords.get(user);
    }

    @Override
    public void close() {
        if (wasOpened) {
            System.out.println("close action");
        }
    }
}
```

#### package validators

```java
package validators;

import exceptions.ValidateException;

public interface Validator {
    void validate(String value) throws ValidateException;
}
```

```java
package validators;

public class NameValidator {
    // допишите код класса
}
```

```java
package validators;

import exceptions.ValidateException;
import exceptions.ValidatePasswordException;

public class PasswordLengthValidator implements Validator {
    private final int minLength;

    public PasswordLengthValidator(final int minLength) {
        this.minLength = minLength;
    }

    @Override
    public void validate(final String password) throws ValidateException {
        if (password == null || password.length() < minLength) {
            throw new ValidatePasswordException(
                    String.format("Пароль должен быть больше %d символов", minLength)
            );
        }
    }
}
```

```java
package validators;

import exceptions.ValidateException;
import exceptions.ValidatePasswordException;

public class PasswordStrengthValidator implements Validator {

    private boolean hasNumber(final String password) {
        for (int counter = 0; counter < password.length(); counter++) {
            if (Character.isDigit(password.charAt(counter))) {
                return true;
            }
        }
        return false;
    }

    private boolean hasLetter(final String password) {
        for (int counter = 0; counter < password.length(); counter++) {
            if (Character.isLetter(password.charAt(counter))) {
                return true;
            }
        }
        return false;
    }

    @Override
    public void validate(final String password) throws ValidateException {
        if (!hasLetter(password) || !hasNumber(password)) {
            throw new ValidatePasswordException("Пароль должен содержать буквы и цифры");
        }
    }
}
```

#### main

```java
import exceptions.ValidateException;
import storage.PasswordMemoryStorage;
import storage.PasswordStorage;
import validators.PasswordLengthValidator;
import validators.PasswordStrengthValidator;
import validators.Validator;

import java.io.IOException;
import java.util.List;
import java.util.Scanner;

public class Practice {

    private static final Scanner scanner = new Scanner(System.in);
    private static final List<Validator> passwordValidators = List.of(
            new PasswordLengthValidator(5), new PasswordStrengthValidator()
    );

    private static final List<Validator> nameValidators = List.of(); // поработайте со списком

    public static void main(String[] args) {
        loop();
    }

    public static void loop() {
        while (true) {
            final String action = getAction();
            if ("1".equals(action)) {
                addUser();
            } else if ("2".equals(action)) {
                showUserPassword();
            } else {
                break;
            }
        }
    }

    private static void checkValidatorRules(
            final List<Validator> validators, final String value
    ) throws ValidateException {
        for (Validator validator : validators) {
            validator.validate(value);
        }
    }

    private static void addUser() {
        final PasswordStorage storage = new PasswordMemoryStorage();
        // добавьте отлов исключений ValidateNameException и ValidatePasswordException
        // закройте хранилище
        try {
            storage.open();
            System.out.println("Введите имя пользователя => ");
            final String name = scanner.nextLine();
            checkValidatorRules(nameValidators, name);
            System.out.println("Введите пароль пользователя => ");
            final String password = scanner.nextLine();
            checkValidatorRules(passwordValidators, password);
            storage.store(name, password);
        } catch (ValidateException e) {
            System.out.println("Ошибка валидации: " + e.getMessage());
        } catch (IOException e) {
            System.out.println("Ошибка работы с хранилищем: " + e.getMessage());
        }
    }

    private static void showUserPassword() {
        final PasswordStorage storage = new PasswordMemoryStorage();
        // добавьте отлов исключения ValidateNameException
        // закройте хранилище
        try {
            storage.open();
            System.out.println("Введите имя пользователя => ");
            final String name = scanner.nextLine();
            checkValidatorRules(nameValidators, name);
            final String password = storage.get(name);
            System.out.println(String.format("Пароль пользователя %s = %s", name, password));
        } catch (ValidateException e) {
            System.out.println("Ошибка валидации: " + e.getMessage());
        } catch (IOException e) {
            System.out.println("Ошибка работы с хранилищем: " + e.getMessage());
        }
    }

    private static String getAction() {
        System.out.println("1 - добавить пользователя с паролем");
        System.out.println("2 - отобразить пароль пользователя");
        System.out.println("другие символы - выход");
        System.out.println("Выберите действие => ");
        return scanner.nextLine();
    }
}
```

_подсказки ниже_

<br><br><br><br><br><br><br><br><br><br><br>

- Класс `ValidateNameException` должен наследовать от `ValidateException` и переопределять его конструктор.
- В методах `open()`, `store()` и `get()` класса `PasswordMemoryStorage` нужно добавить указание на
  исключение `IOException` с помощью `throws`.
- В классе `NameValidator` нужно переопределить метод `validate()`, предупредить об исключении типа `ValidateException`
  и сгенерировать исключение `ValidateNameException`.
- Для генерации исключений используйте ключевое слово `throw`.
- Проверьте, передана ли реализация класса `NameValidator` в список.
- Для отлова исключений `ValidateNameException` и `ValidatePasswordException` в методах `addUser()`
  и `showUserPassword()` нужно использовать блоки `catch`.
- Получить короткое сообщение об ошибке поможет метод `getMessage()`.
- Используйте блок `finally` для закрытия хранилища.