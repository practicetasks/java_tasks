# Задача

Создайте класс `Phone`.

1. **Поля**:
    - `brand` — бренд (строка)
    - `model` — модель (строка)
    - `battery` — уровень заряда батареи (целое число от 0 до 100)

2. **Метод `showInfo()`** — выводит:
   ```
   Телефон: Samsung Galaxy S21
   Заряд: 85%
   ```

3. **Метод `call()`** — уменьшает заряд на `10`, и выводит:
    - Если заряд **после звонка ≥ 10** → `Samsung Galaxy S21 звонит... Заряд: 75%`
    - Если заряд **после звонка < 10** → `Недостаточно заряда для звонка!`

4. **Метод `charge()`** — увеличивает заряд на `20` (но **не больше 100**), и выводит:
    - `Телефон заряжается... Заряд: 100%`

### `main`

```java
public class Test {
    public static void main(String[] args) {
        Phone phone = new Phone();
        phone.brand = "Apple";
        phone.model = "iPhone 14";
        phone.battery = 45;

        phone.showInfo();
        // Телефон: Apple iPhone 14
        // Заряд: 45%
        
        phone.call();   // Apple iPhone 14 звонит... Заряд: 35%
        phone.call();   // Apple iPhone 14 звонит... Заряд: 25%
        phone.charge(); // Телефон заряжается... Заряд: 45%
        phone.call();   // Apple iPhone 14 звонит... Заряд: 35%
    }
}
```
