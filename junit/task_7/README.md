# Задача

Вам предстоит написать тесты чтобы покрывало на 100%

Класс `DrinkVendingMachine` уже реализован
```java
import java.util.HashMap;
import java.util.Map;

public class DrinkVendingMachine {
    private final Map<String, Integer> inventory = new HashMap<>();
    private int balance = 0;

    private static final int DRINK_PRICE = 200;

    public DrinkVendingMachine() {
        inventory.put("Кола", 10);
        inventory.put("Спрайт", 8);
        inventory.put("Фанта", 5);
    }

    public void insertCoin(int value) {
        if (value > 0) {
            balance += value;
        } else {
            throw new IllegalArgumentException("Число должно быть положительным");
        }
    }

    public String selectDrink(String drinkName) {
        if (!inventory.containsKey(drinkName)) {
            return "Такого напитка нет в автомате.";
        }

        int quantity = inventory.get(drinkName);
        if (quantity == 0) {
            return "Извините, " + drinkName + " закончился.";
        }

        if (balance >= DRINK_PRICE) {
            inventory.put(drinkName, quantity - 1);
            balance -= DRINK_PRICE;
            return "Вы получили " + drinkName + "!";
        } else {
            return "Недостаточно средств.";
        }
    }

    public int getDrinkQuantity(String drinkName) {
        return inventory.getOrDefault(drinkName, 0);
    }

    public int getBalance() {
        return balance;
    }
}
```


```java
import org.junit.jupiter.api.Test;

import static org.junit.jupiter.api.Assertions.*;

public class DrinkVendingMachineTest{
    
}
```

_подсказки_

<br><br><br><br><br><br><br><br><br>

Программа должна быть протестирована для всех возможных сценариев, включая:
- Ввод разных номиналов монет.
- Покупка доступного напитка с достаточным балансом.
- Покупка доступного напитка с недостаточным балансом.
- Покупка недоступного напитка.
- Покупка напитка, которого больше нет в наличии.