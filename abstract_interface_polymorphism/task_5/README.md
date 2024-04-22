# Задача

🦉 Дан интерфейс `Openable`, описывающий предметы, которые можно открыть, и два класса: `Can` и `Window`. Доработайте классы
таким образом, чтобы они реализовывали интерфейс `Openable`.


```java
class Can ... {
    ...
    public void open() {
        System.out.println("Чтобы открыть жестяную банку, нужно потянуть кольцо-ключ.");
    }
}

interface Openable {
    void open();
}

public class Practice {     
    public static void main(String[] args) {
        Openable can = new Can();
        can.open();

        Openable window = new Window();
        window.open();
    }
}

class Window ... {
    ...
    public void open() {
        System.out.println("Чтобы открыть окно, нужно повернуть ручку.");
    }
}
```