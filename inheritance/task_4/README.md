## Задача: Система подписок

### Базовый класс Subscription

Поля:
- String userName
- int durationMonths
- boolean autoRenew

Методы:

- double calculatePrice()
    - Базовая цена:

          1000 * durationMonths

- boolean isActive()
  - Подписка активна, если:

        durationMonths > 0

- String getType()
  - Возвращает "Basic"

        void printInfo()

Выводит:

    User: <userName>
    Type: <getType()>
    Duration: <durationMonths> months
    Auto renew: <autoRenew>
    Price: <calculatePrice()>
    Active: <isActive()>


---

### Наследники


#### PremiumSubscription

Доп. поле:
- boolean familyAccess

Логика:
- Базовая цена = super.calculatePrice()
 	- 500 * durationMonths
- если familyAccess == true
- 300 * durationMonths

getType() → "Premium"


#### StudentSubscription

Доп. поле:
- double discountPercent

Логика:
- Цена = super.calculatePrice()
- Скидка не может быть больше 50%
- Если durationMonths >= 12 → дополнительная скидка 10%

getType() → "Student"


#### TrialSubscription

Доп. поле:
- int trialDays

Логика:
- Цена всегда = 0
- Активна только если trialDays > 0
- Если trialDays == 0 → durationMonths считается 0

getType() → "Trial"

---

```java
public class Main {
    public static void main(String[] args) {

        Subscription basic =
                new Subscription("Ali", 3, true);

        PremiumSubscription premium =
                new PremiumSubscription("Dana", 6, false, true);

        StudentSubscription student =
                new StudentSubscription("Arman", 12, true, 60);

        TrialSubscription trial =
                new TrialSubscription("Aruzhan", 0, false, 14);

        basic.printInfo();
        System.out.println();

        premium.printInfo();
        System.out.println();

        student.printInfo();
        System.out.println();

        trial.printInfo();
    }
}
```



Ожидаемый результат

**Basic (Ali)**

3 месяца
- 1000 × 3 = 3000


    User: Ali
    Type: Basic
    Duration: 3 months
    Auto renew: true
    Price: 3000.0
    Active: true


----

**Premium (Dana)**

6 месяцев

База: 1000 × 6 = 6000
- 500 × 6 = 3000
- 300 × 6 = 1800

Итого: 10800

    User: Dana
    Type: Premium
    Duration: 6 months
    Auto renew: false
    Price: 10800.0
    Active: true


--- 

**Student (Arman)**

12 месяцев
- 1000 × 12 = 12000

Скидка 60% → ограничивается до 50%
- 12000 − 6000 = 6000

Доп. скидка 10% (за 12 месяцев):
- 6000 − 600 = 5400

    User: Arman
    Type: Student
    Duration: 12 months
    Auto renew: true
    Price: 5400.0
    Active: true


---

**Trial (Aruzhan)**

trialDays = 14
- Цена всегда 0


      User: Aruzhan
      Type: Trial
      Duration: 0 months
      Auto renew: false
      Price: 0.0
      Active: true

