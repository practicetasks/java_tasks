# Задача

Ваш коллега-программист написал класс `BankAccount`, но не покрыл его функциональность тестами. Коллега давно уволился,
а класс используется практически везде в вашей программе, поэтому просто выкинуть его нельзя. Придётся тестировать!
<br><br>
По остаткам документации вам удалось собрать следующую информацию:

* Чтобы создать `BankAccount`, нужно передать два аргумента — имя и фамилию человека, владеющего счётом.
* Имя владельца можно получить, вызвав метод `getFullName()`. Результат вернётся в виде `String[]`, где по нулевому
  индексу будет имя человека, по первому — фамилия.
* После создания счёт нужно дополнительно активировать при помощи метода `activate(String currency)`. До того как это
  произошло, метод `amount()` будет возвращать ошибку `IllegalStateException("Счёт не активирован.")`,
  а `getCurrency()` — `null`. Активный счёт всегда возвращает `Integer` , отличный от `null`.
* Счёт можно заблокировать вызовом `block`.
* Статус блокировки счёта можно узнать с помощью метода `isBlocked()`.
  <br>

#### Вам необходимо написать 5 тестов:

* `shouldNotBeBlockedWhenCreated` должен проверять, что счёт не заблокирован, после создания стандартного
  объекта `BankAccount` с помощью конструктора.
* `shouldReturnZeroAmountAfterActivation` должен проверять, что счет не заблокирован после активации
  методом `activate(String currency)` с передачей валюты [KZT, EUR, USD], и провеить, что баланс равен 0, а валюта
  счета соответствует переданной.
* `shouldBeBlockedAfterBlockIsCalled` должен проверять, что счёт заблокирован, после вызова метода `block()`.
* `shouldReturnFirstNameThenSecondName` должен проверять, что при вызове метода `getFullName()` возвращается правильный
  массив строк.
* `shouldReturnNullAmountWhenNotActive` должен проверять, что при вызове метода `getAmount()` для неактивного счёта,
  значение `currency` равно `null`, а также выбрасывается исключение `IllegalStateException` с соответствующим
  сообщением.

#### BankAccountTest

```java
import org.junit.jupiter.api.Test;

public class BankAccountTest {

}
```

#### BankAccount

```java
public class BankAccount {

    private boolean isBlocked = false;
    private Integer amount;
    private String currency;

    private final String firstName;
    private final String secondName;

    public BankAccount(String firstName, String secondName) {
        this.firstName = firstName;
        this.secondName = secondName;
    }

    public void block() {
        this.isBlocked = true;
    }

    public void activate(String currency) {
        this.amount = 0;
        this.currency = currency;
    }

    public Integer getAmount() {
        if (amount == null) {
            throw new IllegalStateException("Счёт не активирован.");
        }
        return this.amount;
    }

    public String getCurrency() {
        return currency;
    }

    public boolean isBlocked() {
        return isBlocked;
    }

    public String[] getFullName() {
        return new String[]{firstName, secondName};
    }
}

```