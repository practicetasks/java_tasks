# Задача

Вам предстоит написать тесты чтобы покрывало на 100%

Класс `DrinkVendingMachine` уже реализован
```java
import java.util.HashMap;
import java.util.Map;

public class DrinkVendingMachine {

    private Map<String, Integer> inventory = new HashMap<>();
    private int balance = 0;

    public DrinkVendingMachine() {
        // Заполняем инвентарь напитками
        inventory.put("Кола", 10);
        inventory.put("Спрайт", 8);
        inventory.put("Фанта", 5);
    }

    public void insertCoin(int value) {
        balance += value;
    }

    public String selectDrink(String drinkName) {
        if (inventory.containsKey(drinkName)) {
            int quantity = inventory.get(drinkName);
            if (quantity > 0 && balance >= 200) { 
                inventory.put(drinkName, quantity - 1);
                balance -= 200;
                return "Вы получили " + drinkName + "!";
            } else if (quantity == 0) {
                return "Извините, " + drinkName + " закончился.";
            } else {
                return "Недостаточно средств.";
            }
        } else {
            return "Такого напитка нет в автомате.";
        }
    }

    public int getBalance() {
        return balance;
    }

    public Map<String, Integer> getAvailableDrinks() {
        return inventory;
    }

    public int getDrinkPrice(String drinkName) {
        if (inventory.containsKey(drinkName)) {
            return 200; 
        } else {
            return 0;
        }
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