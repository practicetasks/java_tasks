# Задача

Ваша команда разрабатывает приложение, которое помогает пользователю заполнить заявку на ипотеку. Пользователь вводит
данные для покупки квартиры: фамилию, имя и отчество, возраст, сумму ипотеки и указывает свой статус по трудоустройству.

Задача вашего приложения — проверить данные, которые заполнил пользователь, и показать предварительный ответ банка.
Вам необходимо написать валидацию данных пользователя, используя типизированные классы. Ипотека может быть выдана только
людям 18 лет и старше, минимальная сумма ипотеки — 1.000.000, а максимальная — 10.000.000, человек обязательно должен
быть трудоустроенным.

```java
import java.util.Scanner;

public class Practice {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Заполните данные для ипотечной заявки и узнайте статус одобрения");
        System.out.println("Введите ФИО:");
        String name = scanner.nextLine();

        System.out.println("Ваш возраст:");
        byte age = scanner.nextByte();

        System.out.println("Планируемая сумма ипотеки:");
        int mortgageAmount = scanner.nextInt();

        scanner.nextLine();
        System.out.println("Трудоустроены ли вы сейчас? (д/н)");
        String employedString = scanner.nextLine();
        boolean employed = employedString.equalsIgnoreCase("д");

        MortgageRequest mortgageRequest = new MortgageRequest(name, age, mortgageAmount, employed);
        mortgageRequest.validate();

    }

}
```

```java
// Дополните базовый класс для всех правил валидации
public abstract class ValidationRule {
    protected final ...value;
    private final String errorMessage;

    protected ValidationRule(...value, String errorMessage) {
        this.value = value;
        this.errorMessage = errorMessage;
    }

    public abstract boolean isValid();

    public String getErrorMessage() {
        return errorMessage;
    }
}
```

```java
// Дополните класс для проверки суммы ипотеки пользователя
public class MortgageAmountValidationRule ...{

    public MortgageAmountValidationRule(Integer value) {
        super(value, "Минимальный размер ипотеки - 1.000.000, а максимальный - 10.000.000");
    }

    // Объявите и реализуйте метод для проверки суммы ипотеки ниже
    ...

}
```

```java
// Дополните класс для проверки возраста пользователя
public class AgeValidationRule ...{

    public AgeValidationRule(Byte age) {
        super(age, "Возраст для подачи на ипотеку должен быть старше 18 лет");
    }
    
    @Override
    public boolean isValid() {
        return value >= 18;
    }

}
```

```java
// Дополните класс для проверки трудоустроенности пользователя
public class EmploymentValidationRule ...{

    public EmploymentValidationRule(Boolean value) {
        super(value, "Ипотека выдается только трудоустроенным");
    }
    
    @Override
    public boolean isValid() {
        return value;
    }
}
```

```java
public class MortgageRequest {

    private final String name;
    private final byte age;
    private final int amount;
    private final boolean employed;

    public MortgageRequest(String name, byte age, int amount, boolean employed) {
        this.name = name;
        this.age = age;
        this.amount = amount;
        this.employed = employed;
    }

    public void validate() {
        System.out.println("Проверка заявки...");

        boolean result = true;

        AgeValidationRule ageValidationRule = new AgeValidationRule(age);
        if (!ageValidationRule.isValid()) {
            result = false;
            System.out.println(ageValidationRule.getErrorMessage());
        }

        MortgageAmountValidationRule amountValidationRule = new MortgageAmountValidationRule(amount);
        if (!amountValidationRule.isValid()) {
            result = false;
            System.out.println(amountValidationRule.getErrorMessage());
        }

        EmploymentValidationRule employmentValidationRule = new EmploymentValidationRule(employed);
        if (!employmentValidationRule.isValid()) {
            result = false;
            System.out.println(employmentValidationRule.getErrorMessage());
        }

        if (result) {
            System.out.println(name + ", вам одобрена заявка на ипотеку!");
        } else {
            System.out.println(name + ", ваша заявка отклонена");
        }
    }
}
```

_подсказки ниже_
<br><br><br><br><br><br><br><br><br><br><br><br><br><br>

- Чтобы базовый класс мог принимать значения любого типа, его необходимо сделать типизированным, указав в его объявлении
  параметр типа `T`: `public abstract class ValidationRule<T>`.
- Объявленный параметр типа `T` можно использовать в типизированном классе, когда необходимо указать тип переменной: `T
  value`.
- Чтобы унаследоваться от типизированного класса, необходимо указать ключевое слово `extends`, затем имя базового класс и
  в угловых скобках указать значение параметра типа: `public class AgeValidationRule extends ValidationRule<Byte>`.