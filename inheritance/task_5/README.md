## Задача: Банковские счета и комиссии

### Базовый класс BankAccount

Поля:

- String owner
- double balance

Конструктор:

- owner, balance

Методы:

1. void deposit(double amount)
    - если amount <= 0 → вывести Invalid deposit и ничего не менять
    - иначе увеличить баланс и вывести:
      ```	
      <owner> deposited <amount>. Balance: <balance>
      ```

2. boolean withdraw(double amount)
    - если amount <= 0 → вывести `Invalid withdraw` и вернуть false
    - если денег недостаточно → вывести `Not enough money` и вернуть false
    - иначе уменьшить баланс и вывести:
      ```
      <owner> withdrew <amount>. Balance: <balance>
      ```
      и вернуть true

3. double calculateMonthlyFee()
    - базово 0

4. String getType()
    - "Base"

5. void printReport()
   ```
   Owner: <owner>
   Type: <getType()>
   Balance: <balance>
   Monthly fee: <calculateMonthlyFee()>
   ```

---

## Наследники

### SavingsAccount (накопительный)

Доп. поле:

- double interestPercent (например 5 означает 5%)

Логика:

- calculateMonthlyFee() всегда 0
- Добавить метод applyMonthlyInterest()
- начисляет проценты: balance += balance * (interestPercent / 100) / 12
- вывод:
  ```
  Interest applied. Balance: <balance>
  ```

getType() → "Savings"

--- 

### CheckingAccount (расчётный)

Доп. поле:

- int freeWithdrawals (сколько снятий в месяц бесплатно)
- int withdrawalsThisMonth

Логика:

- Переопределить withdraw(amount):
- если снятие прошло успешно:
- увеличить withdrawalsThisMonth
- если withdrawalsThisMonth > freeWithdrawals → дополнительно списать комиссию 200
- если после комиссии баланс стал < 0 → откатить операцию (вернуть деньги обратно) и вывести:
  ```
  Withdrawal canceled: fee would overdraw account
  ```
- иначе вывести:
  ```
  Fee charged 200. Balance: <balance>
  ```

calculateMonthlyFee():

- если balance < 1000 → 300, иначе 0

getType() → "Checking"

--- 

### BusinessAccount (для бизнеса)

Доп. поле:

- double overdraftLimit (например 5000)

Логика:

- Переопределить withdraw(amount):
- можно уходить в минус до -overdraftLimit
- если нельзя → вывести Overdraft limit exceeded и вернуть false
- иначе снять и вывести как обычно

calculateMonthlyFee() всегда 1000

getType() → "Business"

---


```java
public class Main {
    public static void main(String[] args) {
        SavingsAccount sa = new SavingsAccount("Ali", 12000, 6);
        CheckingAccount ca = new CheckingAccount("Dana", 1500, 2);
        BusinessAccount ba = new BusinessAccount("Shop", 1000, 5000);

        sa.printReport();
        sa.applyMonthlyInterest();
        sa.withdraw(2000);
        System.out.println();

        ca.printReport();
        ca.withdraw(200);
        ca.withdraw(200);
        ca.withdraw(200); // тут должна быть комиссия
        System.out.println();

        ba.printReport();
        ba.withdraw(5500); // должен уйти в минус, но в пределах лимита
        ba.withdraw(1000); // должен превысить лимит
    }
}
```
#### Ожидаемый результат

(числа могут быть с .0 — это нормально)

```
Owner: Ali
Type: Savings
Balance: 12000.0
Monthly fee: 0.0
Interest applied. Balance: 12060.0
Ali withdrew 2000.0. Balance: 10060.0

Owner: Dana
Type: Checking
Balance: 1500.0
Monthly fee: 0.0
Dana withdrew 200.0. Balance: 1300.0
Dana withdrew 200.0. Balance: 1100.0
Dana withdrew 200.0. Balance: 900.0
Fee charged 200. Balance: 700.0

Owner: Shop
Type: Business
Balance: 1000.0
Monthly fee: 1000.0
Shop withdrew 5500.0. Balance: -4500.0
Overdraft limit exceeded
```

