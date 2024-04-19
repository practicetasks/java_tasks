# Задача

Помогите пользователю вашего приложения связаться с другом через виртуальную АТС. Допишите модуль АТС, используя принципы полиморфизма. <br> <br>
Способ связи будет зависеть от модели телефона, принимающего вызов пользователя.  <br> <br>
Если у пользователя стационарный или мобильный телефон, то позвонить ему можно только по сотовой связи (в этом случае необходимо вывести сообщение `Набираем номер <targetNumber> и звоним по сотовой связи)`.  <br> <br>
Любой смартфон — это мобильный телефон, но не любой мобильный телефон — смартфон! У смартфона есть возможность принимать звонки и сообщения как по сотовой связи, так и через сторонние приложения — в этом случае перед звонком нужно вывести сообщение Позвоним через приложение <appName> по номеру <targetNumber>.  <br> <br>
Если у пользователя мобильный телефон, ему можно отправить SMS: `Отправляем сообщение <messageText> по номеру <targetNumber>`.  <br> <br>
А пользователь смартфона может отправлять не только SMS, но и email — в этом случае нужно вывести сообщение `Напишем другу сообщение <messageText> по email`.  <br> <br>

<br>
<br>

#### Базовый класс Phone

```java
public class Phone {
    private final String number;

    public Phone(String number) {
        this.number = number;
    }

    public final void makeCall(String targetNumber) {
        System.out.println("Звоним с номера " + number);
        System.out.println("Набираем номер " + targetNumber + " и звоним по сотовой связи");
        System.out.println("Привет!");
    }
}
```

<br>
<br>

#### Smartphone

```java
// Допишите реализацию класса Smartphone
public class Smartphone {

    ...

    public final void sendEmail(String email, String messageText) {
        System.out.println("Напишем другу сообщение " + messageText + " по email " + email);
    }

}
```


<br>
<br>

#### MobilePhone

```java
public class MobilePhone {
    ...

    public final void sendSms(String targetNumber, String messageText) {
        System.out.println("Отправляем сообщение " + messageText + " по номеру " + targetNumber);
    }
}
```


<br>
<br>

#### CellularPhone

```java
// Допишите реализацию класса CellularPhone
public class CellularPhone {

}
```

<br>
<br>

#### Main

```java
import java.util.Scanner;

public class Practice {

    public static void main(String[] args) {
        System.out.println("Вас приветствует виртуальная АТС!");

        Scanner scanner = new Scanner(System.in);
        System.out.println("Введите ваш номер телефона:");
        String number = scanner.next();
        System.out.println("Введите номер пользователя, которому хотите позвонить:");
        String friendNumber = scanner.next();
        System.out.println("Выберите модель телефона собеседника, 1 - стационарный телефон, 2 - мобильный телефон, 3 - смартфон:");
        int type = scanner.nextInt();

        if (type < 1 || type > 3) {
            System.out.println("Введена неверная модель телефона");
            return;
        }

        getPhone(type, number).makeCall(friendNumber);
    }

    public static ... getPhone(int type, String number) {
        if (...) {
            // Если выбран стационарный телефон, создайте объект класса CellularPhone
            return new CellularPhone(number);
        } else if (...) {
            // Если выбран мобильный телефон, создайте объект класса MobilePhone
            return new MobilePhone(number);
        } else {
            // Иначе создайте экземпляр класса Smartphone
            ...
        }
    }

}
```
