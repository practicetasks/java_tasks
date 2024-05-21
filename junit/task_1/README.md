# Задача

На текущий момент класс `DiscountCalculatorTest` покрывает только один тест-кейс из пяти. Составьте ещё четыре теста,
чтобы обеспечить полное покрытие класса `DiscountCalculator`.
Вам нужно покрыть все тест-кейсы из списка:
Если покупка на сумму 1–999 тенге, то скидка составляет 0%.

1.1. Совершить покупку на 1 тенге. Ожидаемое поведение: стоимость покупки составляет 1 тенге.

1.2. Совершить покупку на 333 тенге. Ожидаемое поведение: стоимость покупки составляет 333 тенге.

1.3. Совершить покупку на 999 тенге. Ожидаемое поведение: стоимость покупки составляет 999 тенге.
Иначе скидка составляет 2%.

2.1. Совершить покупку на 1000 тенге. Ожидаемое поведение: стоимость покупки составляет 980 тенге (-2%).

2.2. Совершить покупку на 2000 тенге. Ожидаемое поведение: стоимость покупки составляет 1960 тенге (-2%).

Наименование тестовых методов уже представлено в классе `DiscountCalculatorTest`.


```java
public class DiscountCalculator {
    public int sumAfterDiscount(int sum) {
        if (sum < 1000) {
            return sum;
        } else {
            return (int) (sum * 0.98);
        }
    }
}
```

```java
import org.junit.jupiter.api.Assertions;
import org.junit.jupiter.api.Test;

public class DiscountCalculatorTest {

    DiscountCalculator discountCalculator = new DiscountCalculator();

    @Test
    public void shouldGiveNoDiscountForValue999() {
        // Подготовка
        int buySum = 999;
        int expectedSum = 999;

        // Исполнение
        int resultSum = discountCalculator.sumAfterDiscount(buySum);

        // Проверка
        Assertions.assertEquals(expectedSum, resultSum);
    }

    @Test
    public void shouldGiveNoDiscountForValue1() {
    }

    @Test
    public void shouldGiveNoDiscountForValue333() {
    }

    @Test
    public void shouldGive2PercentDiscountForValue1000() {
    }

    @Test
    public void shouldGive2PercentDiscountForValue2000() {
    }
}
```