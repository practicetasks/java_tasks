# Задача

Попрактикуемся с методами в коде. Метод `requestUserName` запрашивает у пользователя его имя (пока мы оставили за кадром
эту часть логики и предполагаем, что полученное имя попало в переменную `username`). Затем имя пользователя отображается
на экране. Но мы допускаем, что пользователь хочет сохранить своё имя в тайне, — и поэтому метод `requestUserName`
возвращает тип `Optional`. Ваша задача — реализовать недостающий код по работе с `Optional`-значениями.

```java
import java.util.Optional;

public class OptionalNameDemo {
    static Optional<String> requestUserName() {
        //Здесь должен быть запрос к пользователю, но пока его не реализовали
        //Поместите в переменную username имя пользователя или оставьте ее пустой, если имя скрыто
        String username = "";

        if (username.isBlank()) {
            //вставьте код здесь
        } else {
            //вставьте код здесь
        }
    }

    public static void main(String[] args) {
        Optional<String> maybeName = requestUserName();
        if (/*вставьте код здесь*/) {
            //вставьте код здесь
            System.out.println("Привет, " + name + "!");
        } else {
            System.out.println("Ваше право не называть имя!");
        }
    }
}
```

_подсказки ниже :)_

<br><br><br><br><br><br><br><br><br><br>

- В методе `requestUserName` используйте методы `Optional.of` и `Optional.empty`, чтобы «обернуть» прочитанное имя
  пользователя в `Optional`.
- Извлечь имя из `Optional` помогут методы `isPresent()` и `get()`.
