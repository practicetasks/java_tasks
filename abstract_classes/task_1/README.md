# Задача

Даны два класса, описывающие поведение уток — летающей и резиновой. Их поведение в чём-то совпадает, а чем-то
различается. Выделите абстрактный класс `Duck`, который будет содержать общие свойства и методы обоих классов.


```java
// Выделите абстрактный класс Duck,
// который будет содержать общие свойства и методы классов FlyingDuck и RubberDuck
class Duck {
}

class FlyingDuck {

    public String getName() {
        return "Я - обычная утка. Кря!";
    }

    public void swim() {
        System.out.println("Да, я умею плавать!");
    }

    public void fly() {
        System.out.println("Лечу куда хочу.");
    }

    public void eat() {
        System.out.println("Обычно кушаю разные семена, но иногда нахожу хлебушек.");
    }

    public void quack() {
        System.out.println("Кря!");
    }
}

class RubberDuck {

    public String getName() {
        return "Я - резиновая уточка!";
    }

    public void swim() {
        System.out.println("Да, я умею плавать!");
    }

    public void quack() {
        System.out.println("Кря!");
    }
}


public class Practice {
    public static void main(String[] args) {
        FlyingDuck flyingDuck = new FlyingDuck();
        RubberDuck rubberDuck = new RubberDuck();

        System.out.println("Сначала о себе расскажет обычная уточка:");
        System.out.println(flyingDuck.getName());
        flyingDuck.swim();
        flyingDuck.fly();
        flyingDuck.eat();
        flyingDuck.quack();

        System.out.println("А теперь - резиновая:");
        System.out.println(rubberDuck.getName());
        rubberDuck.swim();
        rubberDuck.quack();
    }
}
```