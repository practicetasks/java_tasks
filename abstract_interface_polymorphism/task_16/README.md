# Задача: Система оплаты

Есть разные способы оплаты.
Все они должны уметь обрабатывать платёж, но делают это по-разному.


### Базовый класс Payment

Поля
- String account
- double balance

Конструктор
- Принимает account, balance.

Методы

- boolean pay(double amount)
  Логика по умолчанию:
  - если amount <= 0

    вывести
    ```
    Invalid payment
    ```

  - если balance < amount
    ```
    Payment failed: insufficient funds
    ```
  - иначе:
    ```
    Payment of <amount> from <account> successful
    ```
и уменьшить баланс.

---


void printBalance()

Account: <account>, Balance: <balance>


---

## Наследники

### CardPayment

Доп. поле
- double commissionPercent

Логика pay():
- комиссия:
  ```
  amount * commissionPercent / 100
  ```
- итоговая сумма списания = amount + commission
- если денег не хватает → платёж не проходит
- если проходит → вывести
  ```
  Card payment <amount> processed. Commission: <commission>
  ```


---

### BankTransfer

Доп. поле
- double transferFee

Логика pay():
- итоговое списание = amount + transferFee

    Вывод:
    ```
    Bank transfer <amount> completed. Fee: <transferFee>
    ```

---

### MobilePayment

Доп. поле
- double dailyLimit

Логика pay():
- если amount > dailyLimit
  ```
  Payment exceeds daily limit
  ```

- иначе обычная оплата 
  ```
  Mobile payment <amount> successful
  ```
  


---

### Main

Создаём массив Payment:
```java
public class Main {
    public static void main(String[] args) {

        Payment[] payments = {
                new CardPayment("CARD-001", 5000, 2),
                new BankTransfer("BANK-ABC", 8000, 150),
                new MobilePayment("PHONE-777", 2000, 1000)
        };

        for (Payment payment : payments) {
            payment.printBalance();
            payment.pay(900);
            payment.printBalance();
            System.out.println();
        }
    }
}
```


----

##### Ожидаемый результат

```
Account: CARD-001, Balance: 5000
Card payment 900.0 processed. Commission: 18.0
Account: CARD-001, Balance: 4082.0

Account: BANK-ABC, Balance: 8000
Bank transfer 900.0 completed. Fee: 150.0
Account: BANK-ABC, Balance: 6950.0

Account: PHONE-777, Balance: 2000
Mobile payment 900.0 successful
Account: PHONE-777, Balance: 1100.0
```

