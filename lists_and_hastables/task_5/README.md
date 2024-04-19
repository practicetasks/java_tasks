# Задача
В хеш-таблице `customersOrders` класса `OrdersManager` собрана информация о клиентах зоомагазина (это ключи) и их заказах. 
Дополните код методов:
1. В `printAllOrders()` и `getOrdersSum()`, которые печатают список всех заказов и возвращают их общую сумму, вызовите нужные методы `HashMap`.
2. В методе `printCustomerOrders(String customerName)` перед печатью заказов конкретного клиента добавьте проверку наличия его имени в таблице. Это нужно, чтобы избежать ошибки ссылки на `null`.
3. Метод `getMaxOrderCustomerName()` должен возвращать имя клиента, который потратил в зоомагазине больше всего. Переменные для хранения имени клиента и максимальной суммы заказов мы объявили и инициализировали за вас. Числовое переменной присвоили 0, а строковой — пустую строку `""`. Вам нужно дописать логику работы метода. Вы уже не раз искали максимум в массивах или списках. Здесь получится очень похоже!
4. Метод `removeUnprofitableOrders` должен удалять из таблицы клиентов, сумма заказов которых строго меньше 5000.

#### OrdersManager
```java
import java.util.ArrayList;
import java.util.HashMap;

public class OrdersManager {
    HashMap<String, ArrayList<Double>> customersOrders;

    public OrdersManager() {
        customersOrders = new HashMap<>();
        ArrayList<Double> orders = new ArrayList<>();
        orders.add(154.43);
        orders.add(5453.98);
        orders.add(8776.65);
        customersOrders.put("Иван И.", orders);

        orders = new ArrayList<>();
        orders.add(25343.54);
        orders.add(420.50);
        customersOrders.put("Ольга С.", orders);

        orders = new ArrayList<>();
        orders.add(325.90);
        customersOrders.put("Александр Т.", orders);

        orders = new ArrayList<>();
        orders.add(253.54);
        orders.add(420.50);
        customersOrders.put("Александр Р.", orders);

        orders = new ArrayList<>();
        orders.add(780.54);
        orders.add(420.50);
        orders.add(36343.54);
        orders.add(2000.50);
        customersOrders.put("Екатерина О.", orders);
    }

    void printAllOrders() {
        for (String name : ...) { // Цикл должен пройтись по ключам
            System.out.println("Заказы " + name + ":");
            ArrayList<Double> value = customersOrders.get(name);
            System.out.println(value);
        }
    }

    double getOrdersSum() {
        double sum = 0;
        for (ArrayList<Double> orders : ...) { // Здесь должен быть обход по значениям
            for (double orderPrice : orders) {
                sum += orderPrice;
            }
        }
        return sum;
    }

    void printCustomerOrders(String customerName) {
        if (...) { // Проверьте, есть ли указанный ключ в таблице
            System.out.println("Заказы " + customerName + ":");
            System.out.println(customersOrders.get(customerName));
        }
    }

    String getMaxOrderCustomerName() {
        double maxOrder = 0;
        String customerName = "";

        ... // Допишите логику работы метода

        return customerName;
    }

    void removeUnprofitableOrders() {
        ArrayList<String> names ... // Создайте список клиентов с заказами меньше 5000
        
        // Наполните список names
        for ...

            double ordersSum = 0;
            for ...

            if (ordersSum < 5000) {
                ...
            }
        }

        for ... // Удалите из хеш-таблицы тех, чьи расходы не превышают 5000
           
            System.out.println("Клиента " + name + " больше нет в таблице.");
        }
    }
}
```


#### main
```java
public class Practice {
    public static void main(String[] args) {
        OrdersManager ordersManager = new OrdersManager();

        ordersManager.printAllOrders();
        System.out.println("Всего заказов на сумму: " + ordersManager.getOrdersSum());

        String maxOrderCustomerName = ordersManager.getMaxOrderCustomerName();
        System.out.println("Самая большая сумма заказов у " + maxOrderCustomerName);
        ordersManager.printCustomerOrders(maxOrderCustomerName);

        ordersManager.removeUnprofitableOrders();
    }
}
```



<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

###### Подсказки
* Для получения ключей из таблицы вам понадобится метод `keySet()`.
* Для получения всех значений в таблице вам понадобится метод `values()`.
* Для проверки имени клиента воспользуйтесь методом `containsKey(customerName)`.
* Чтобы найти клиента с наибольшей суммой заказов, пройдите по всем клиентам и посчитайте их суммы заказов — это можно сделать с помощью вложенных циклов for. Внутри второго цикла сравнивайте суммы заказов и сохраняйте наибольшую и имя клиента. Так вы получите искомый результат.
* Чтобы найти клиентов, чьи заказы меньше 5000, пройдите по ключам таблицы с помощью цикла for: `for (String name : customersOrders.keySet())`. Затем получите сумму заказа. Проверьте её с помощью `if`.
* С помощью ещё одного `for` пройдите по полученному списку с именами клиентов, чьи заказы меньше 5000 `for (String name : names)`, и через метод `remove` удалите их из таблицы.