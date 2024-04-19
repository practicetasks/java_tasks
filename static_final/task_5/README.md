# Задача

Перед вами метод `getPopulationPercent`. Он принимает на вход название континента и возвращает процент живущих на нём
людей от общего числа населения планеты.

Перепишите код так, чтобы в нём использовался оператор `switch`.

```java
public class Practice {
    public static void main(String[] args) {
        System.out.println(getPopulationPercent(Continent.ASIA));
    }

    public static String getPopulationPercent(Continent continent) {
        String result;

        if (continent == Continent.ASIA) {
            result = "59.5%";
        } else if (continent == Continent.AFRICA) {
            result = "16.9%";
        } else if (continent == Continent.NORTH_AMERICA) {
            result = "7.7%";
        } else if (continent == Continent.SOUTH_AMERICA) {
            result = "5.6%";
        } else if (continent == Continent.ANTARCTICA) {
            result = "<0.1%";
        } else if (continent == Continent.EUROPE) {
            result = "9.7%";
        } else if (continent == Continent.AUSTRALIA) {
            result = "0.5%";
        } else {
            result = "Такого материка не существует.";
        }

        return result;
    }
}

enum Continent {
    ASIA,
    AFRICA,
    NORTH_AMERICA,
    SOUTH_AMERICA,
    ANTARCTICA,
    EUROPE,
    AUSTRALIA
}
```