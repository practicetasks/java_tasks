Значения статических переменных меняются довольно хитро.
В представленном ниже кусочке кода переменные `nonStaticVariable` и 
`staticVariable` отличаются только модификатором `static`,
а логика работы с ними — одинаковая. 
Ваша задача — проанализировать код и определить,
чему будут равны значения переменных `nonStaticVariable`
и `staticVariable` для объекта `counter2`.
<br>
<br>

```java
public class Counter {

    private int nonStaticVariable = 0; 
    private static int staticVariable = 0; 

    public void addTen() {
        nonStaticVariable += 10;
        staticVariable += 10;
    }

    public static void main(String[] args) {
        Counter counter1 = new Counter();
        counter1.addTen();

        Counter counter2 = new Counter();
    }
}
```

#### Варианты ответов
a) 0, 0 <br>
b) 0, 10 <br>
c) 10, 0 <br>
d) 10, 10 <br>