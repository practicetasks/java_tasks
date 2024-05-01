# Задача

Новый год — это всегда суета, огромное число подарков и поздравлений. Родные, друзья, коллеги, одногруппники.
Приложение `NewYearReminder` напомнит о приближении Нового года и поможет с поздравлениями. Пользователю нужно только
указать имя `<contact>`, остальное приложение берёт на себя.

Чтобы поздравить близких друзей, им нужно позвонить и позвать на кофе. Чтобы поздравить коллег, нужно отправить
электронное письмо с новогодней картинкой через корпоративную почту. Одногруппники порадуются стикеру в социальных
сетях. А родственники в любом уголке планеты оценят бумажную открытку в почтовом ящике.

Приложение работает с адресной книгой в телефоне, по тегам оно создаёт четыре списка контактов `ContactBook`.

Допишите код приложения так, чтобы пользователи могли поздравить любого человека из своей телефонной книги, просто
указав его имя.

### Базовый класс Contact

```java
// Дополните объявление класса Contact
public ... Contact {
    // Класс должен содержать одно поле - имя пользователя name
    ...

    // И два метода - sendMessage() для отправки сообщения и print() для печати информации о контакте
    ...
}
```

##### класс Email

```java
// Унаследуйте класс от базового класса, описывающего контакт Contact
public class Email ... {
    private final String email;
    
    public Email(String name, String email) {
        ...
        this.email = email;
    }
    
    public String getEmail() {
        return email;
    }
    
    // Метод sendMessage переопределяет метод базового класса
    ...
    public void sendMessage() {
        System.out.println("Отправим новогоднюю картинку коллеге на электронную почту " + email);
    }
        
    ...
    public void print() {
        System.out.println("Email: " + getEmail());
    }
}
```

##### класс Phone

```java
// Унаследуйте класс от базового класса, описывающего контакт Contact
public class Phone ... {
    private final String phoneNumber;
    
    public Phone(String name, String phoneNumber) {
        ...
        this.phoneNumber = phoneNumber;
    }
    
    public String getPhoneNumber() {
        return phoneNumber;
    }
    
    // Метод sendMessage переопределяет метод базового класса
    ...
    public void sendMessage() {
        System.out.println("Звоним другу по номеру " + phoneNumber + " и зовем на кофе.");
    }
        
    ...
    public void print() {
        System.out.println("Номер телефона: " + getPhoneNumber());
    }
}
```

##### класс SocialNetworkContact

```java
// Унаследуйте класс от базового класса, описывающего контакт Contact
public class SocialNetworkContact ... {
    private final String socialNetwork;
    private final String username;
    
    public SocialNetworkContact(String name, String socialNetwork, String username) {
        ...
        this.socialNetwork = socialNetwork;
        this.username = username;
    }
    
    public String getSocialNetwork() {
        return socialNetwork;
    }
    
    public String getUsername() {
        return username;
    }
    
    // Метод sendMessage переопределяет метод базового класса
    ...
    public void sendMessage() {
        System.out.println("Отправим забавный стикер одногруппнику в соцсети " + socialNetwork + ", имя пользователя " + username);
    }
        
    ...
    public void print() {
        System.out.println("Социальная сеть: " + socialNetwork);
        System.out.println("Имя пользователя: " + username);
    }
}
```

##### класс Address

```java
// Унаследуйте класс от базового класса, описывающего контакт Contact
public class Address ... {
    private final String city;
    private final String address;
    
    public Address(String name, String city, String address) {
        ...
        this.city = city;
        this.address = address;
    }
    
    public String getCity() {
        return city;
    }
    
    public String getAddress() {
        return address;
    }
    
    // Метод sendMessage переопределяет метод базового класса
    ...
    public void sendMessage() {
        System.out.println("Отправим открытку в город " + city + " по адресу: " + address);
    }
        
    ...
    public void print() {
        System.out.println("Город: " + getCity());
        System.out.println("Адрес: " + getAddress());
    }
}
```

##### класс ContactBook

```java
// Ограничьте класс ContactBook так, чтобы он мог хранить в себе только список контактов
public class ContactBook ... {
    // Объявите поле класса contacts - список контактов книги
    ...

    public void addContact(...contact) {
        contacts.add(contact);
    }
    
    public void printList() {
        // Выведите на экран весь список контактов книги
        ...
        System.out.println("Имя: " + contact.getName());
        contact.print();
    }
    
    public void congratulate(String name) {
        boolean contactPresented = false; //проверяем есть ли контакт в базе
        // Найдите контакт в книге по имени, и отправьте ему сообщение с помощью метода sendMessage()
        ...
        System.out.println("Поздравим с Новым годом ваш контакт из записной книжки: " + name);
        contact.sendMessage();
    
        // Если контакт не найден, выведите соответсвующее сообщение
        System.out.println("Не найден контакт с указанным именем.");
    }
}
```

##### main

```java
import java.util.Scanner;

public class Practice {

    // Дополните объявление поля friendsContactBook, которое будет хранить в себе список номеров телефонов друзей
    private static ContactBook...friendsContactBook =...
    // Напишите объявления полей colleaguesContactBook, classmatesContactBook и relativesContactBook,
    // которые будут хранить списки электронных адресов, соцсетей и почтовых адресов соответственно
    ...


    public static void main(String[] args) {
        fillBooks();

        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("Сегодня Новый Год! 1 - Отправить поздравление, 0 - Напомнить позднее");
            int mainCommand = scanner.nextInt();
            if (mainCommand == 1) {
                System.out.println("Какую книгу контактов открыть?");
                System.out.println("1 - Друзья, 2 - Коллеги, 3 - Одногруппники, 4 - Родственники");

                int bookIndex = scanner.nextInt();
                if (bookIndex == 1) {
                    friendsContactBook.printList();
                } else if (bookIndex == 2) {
                    colleaguesContactBook.printList();
                } else if (bookIndex == 3) {
                    classmatesContactBook.printList();
                } else if (bookIndex == 4) {
                    relativesContactBook.printList();
                }

                System.out.println("Кого вы хотите поздравить? Введите имя:");
                String name = scanner.next();
                if (bookIndex == 1) {
                    friendsContactBook.congratulate(name);
                } else if (bookIndex == 2) {
                    colleaguesContactBook.congratulate(name);
                } else if (bookIndex == 3) {
                    classmatesContactBook.congratulate(name);
                } else if (bookIndex == 4) {
                    relativesContactBook.congratulate(name);
                }
            } else if (mainCommand == 0) {
                break;
            }
        }
    }

    private static void fillBooks() {
        friendsContactBook.addContact(new Phone("Асылбек", "+7-707-000-11-22"));
        friendsContactBook.addContact(new Phone("Малика", "+7-777-555-11-22"));
        friendsContactBook.addContact(new Phone("Куандык", "+7-702-698-00-22"));

        colleaguesContactBook.addContact(new Email("Александр", "sasha@sasha.org"));
        colleaguesContactBook.addContact(new Email("Павел", "pasha@pasha.org"));
        colleaguesContactBook.addContact(new Email("Олег", "oleg@oleg.com"));

        classmatesContactBook.addContact(new SocialNetworkContact("Анита", "НаСвязи", "anita"));
        classmatesContactBook.addContact(new SocialNetworkContact("Жека", "Фотопризма", "zheka"));

        relativesContactBook.addContact(new Address("Бабуля", "Астана", "Кабанбай батыра, 58"));
        relativesContactBook.addContact(new Address("Дедуля", "Алматы", "Ленина, д.10"));
    }

}
```

_подсказки ниже_
<br><br><br><br><br><br><br><br><br><br><br><br><br>

- В программе не требуется использовать объекты класса `Contact`, только его наследников, поэтому класс `Contact` можно
  объявить абстрактным: `public abstract class Contact`.
- Реализации методов `sendMessage()` и `print()` будут отличаться для каждого конкретного типа контакта, поэтому в
  базовом
  классе `Contact` эти методы нужно объявить абстрактными.
- Чтобы унаследовать класс от абстрактного, воспользуйтесь ключевым словом `extends`: `public class Address extends
  Contact`.
- Чтобы обратиться к конструктору суперкласса, используйте ключевое слово `super`: `super(name)`.
- Чтобы класс `ContactBook` мог хранить в себе только определённый тип контактов, его необходимо сделать типизированным
  с
  ограничением на тип: `public class ContactBook<T extends Contact>`.
- Для вывода на экран списка контактов воспользуйтесь циклом `for`: `for (T contact : contacts) {...}`.