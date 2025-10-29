# Задача

1. Базовый класс Animal
   Поля:

- `String name` — имя животного.
  Конструктор, принимающий name.
  Методы:
- void `makeSound()` — по умолчанию выводит в консоль что-то вроде `"Some generic animal sound"`.
- void `printInfo()` — выводит в консоль name и затем вызывает `makeSound()`.

2. Классы-наследники
    - Dog
        - Переопределяет makeSound(), чтобы выводить "Woof!".
        - Добавьте метод void fetch() — печатает "Dog <name> is fetching the ball!".

    - Cat
        - Переопределяет makeSound(), чтобы выводить "Meow!".
        - Добавьте метод void scratch() — печатает "Cat <name> is scratching the sofa!".
    - Cow
        - Переопределяет makeSound(), чтобы выводить "Moo!".
```java
public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog("Rex");
        System.out.println("Animal name: " + dog.getName());
        dog.makeSound();
        dog.fetch();

        Cat cat = new Cat("Whiskers");
        System.out.println("Animal name: " + cat.getName());
        cat.makeSound();
        cat.scratch();

        Cow cow = new Cow("Bessie");
        System.out.println("Animal name: " + cow.getName());
        cow.makeSound();
    }
}
```

Пример ожидаемого вывода

```
Animal name: Rex
Woof!
Dog Rex is fetching the ball!

Animal name: Whiskers
Meow!
Cat Whiskers is scratching the sofa!

Animal name: Bessie
Moo!
```

