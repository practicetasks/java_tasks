# Задача

Дан код программы, которая окрашивает точку с заданными координатами в нужный цвет и выводит получившийся результат на
консоль. Изучите код программы и определите, какой результат будет выведен в результате выполнения программы после
заголовка "Заданная точка была окрашена:"?

```java
public class Practice {
    public static void main(String[] args) {
        // Координаты точки
        int x = 4;
        int y = 2;
        // Цвет точки
        String color = "розовый";

        Point point = new ColorPoint(x, y, color);

        System.out.println("Заданная точка была окрашена: " + point.getName());
    }
}

class ColorPoint extends Point {
    private final String color;

    public ColorPoint(int x, int y, String color) {
        super(x, y);
        this.color = color;
        // Какой из методов makeName() здесь будет вызван - родительского класса или класса-наследника?
        setName(makeName());
    }

    @Override
    protected String makeName() {
        // Какое значение цвета будет у объекта в момент вызова этого метода?
        return "координаты " + super.makeName() + ", цвет " + color;
    }
}

class Point {
    private final int x;
    private final int y;
    private String name;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public void setName(String name) {
        this.name = name;
    }

    protected String makeName() {
        return "(" + x + "," + y + ")";
    }

    public String getName() {
        return name;
    }
}
```