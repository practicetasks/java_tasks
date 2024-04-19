# Задача

Часто при обновлении программ необходимо поддерживать старый код. Доработайте код новой версии игры-стратегии, чтобы он поддерживал параметры из старой версии:

* Поле `gold` типа `long` необходимо сохранить в переменную `characterGold` типа `int` (точно известно, что значение параметра `gold` меньше 2 000 000 000).
* Поле `silver` типа `byte` необходимо сохранить как переменную `characterSilver` типа `int`, предварительно умножив её на 100.
* Поле `wood` типа `short` необходимо сохранить как переменную `characterWood` типа `double`.
* Поле `health` типа `long` необходимо сохранить как переменную `characterHealth` типа `byte` (точно известно, что значение параметра `health` меньше 100).
* Поле `hasHelper` типа `boolean` необходимо сохранить как переменную `characterHelpersNumber` типа `byte`. Если параметр `hasHelper` равен `true`, то в переменную `characterHelpersNumber` сохранить единицу, если `false` — ноль.

### Класс Character
```java
class Character {
    int gold;
    int silver;
    double wood;
    byte health;
    byte helpersNumber;

    public Character(
            int characterGold,
            int characterSilver,
            double characterWood,
            byte characterHealth,
            byte characterHelpersNumber
    ) {
        gold = characterGold;
        silver = characterSilver;
        wood = characterWood;
        health = characterHealth;
        helpersNumber = characterHelpersNumber;
    }
}
```


### Класс Resources
```java
class Resources {
    long gold;
    byte silver;
    short wood;
    long health;
    boolean hasHelper;

    public Resources(
            long inputGold,
            byte inputSilver,
            short inputWood,
            long inputHealth,
            boolean inputHasHelper
    ) {
        gold = inputGold;
        silver = inputSilver;
        wood = inputWood;
        health = inputHealth;
        hasHelper = inputHasHelper;
    }
}
```


### main
```java
public class Practice {
    public static void main(String[] args) {
        long inputGold = 200L;
        byte inputSilver = 39;
        short inputWood = 2005;
        long inputHealth = 97L;
        boolean inputHasHelper = true;

        Resources characterResources = new Resources(
                inputGold,
                inputSilver,
                inputWood,
                inputHealth,
                inputHasHelper
        );

        int characterGold = ...
        int characterSilver = ...
        double characterWood = ...
        byte characterHealth = ...
        byte characterHelpersNumber;

        // Установка значения characterHelpersNumber в зависимости от значения hasHelper
        ...

        Character character = new Character(
                characterGold,
                characterSilver,
                characterWood,
                characterHealth,
                characterHelpersNumber
        );

        System.out.println("Персонаж создан успешно!");
        System.out.println("Количество золота: " + character.gold);
        System.out.println("Количество серебра: " + character.silver);
        System.out.println("Количество дерева: " + character.wood);
        System.out.println("Здоровье: " + character.health);
        System.out.println("Количество помощников: " + character.helpersNumber);
        System.out.println("Навстречу приключениям!");
    }
}
```