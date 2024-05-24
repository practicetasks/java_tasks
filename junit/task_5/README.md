# Задача

**Обратная польская нотация** (англ. _Reverse Polish notation, RPN_) — способ записи математических выражений, при
котором
операнды (числа) записываются перед знаками операций. Например, запись `4 3 +` обозначает, что нужно сложить числа `4`
и `3`,
а запись `1 2 3 - +` исполнится в два этапа. Сначала из числа `2` нужно вычесть `3`, что упростит выражение до `1 -1 +`,
а затем
сложить `-1` с `1` и получить `0`.

При обратной польской нотации операции не имеют приоритета, а результат выражения можно считать слева направо. Всякий
раз, когда встречается новая операция, необходимо исполнить её над двумя последними операндами, а затем записать
результат вместо этой операции и двух операндов.

В качестве примера для вас реализован алгоритм обратной польской нотации, поддерживающий операции `+, -, *`, а также
отрицательные числа. Выражение в польской нотации должно передаваться в виде строки, где операнды и операции разделены
произвольным количеством пробелов. Напишите набор тест-кейсов для проверки этой реализации. В данном примере вам не
нужно разбираться в коде `ReversePolishNotationCalculator`. Достаточно проверить, что код работает для
операций `+, -, *`, а
также что он правильно обрабатывает пробельные символы и отрицательные числа.

Для прохождения этого задания вам необходимо обеспечить 100% покрытие кода для этого примера.

💡 Если вместо покрытия кода сфокусироваться на покрытии требований к программе, с высокой вероятностью это приведёт к
100% покрытию кода.


```java
import java.util.ArrayDeque;
import java.util.Deque;

import org.junit.jupiter.api.Test;

public class ReversePolishNotationCalculatorTest {

    @Test
    public void shouldCalculateAddition() {

    }
}

class ReversePolishNotationCalculator {
    public int calculatePolishNotation(String str) {
        String[] parts = str.split(" ");
        Deque<Integer> numbers = new ArrayDeque<>();
        int index = 0;

        while (index != parts.length) {

            if (parts[index].isBlank()) {
                index++;
                continue;
            }

            if (isOperation(parts[index])) {
                int operandOne = numbers.pop();
                int operandTwo = numbers.pop();

                if (parts[index].equals("+")) {
                    numbers.push(operandOne + operandTwo);
                } else if (parts[index].equals("-")) {
                    numbers.push(operandTwo - operandOne);
                } else if (parts[index].equals("*")) {
                    numbers.push(operandOne * operandTwo);
                }

            } else {
                numbers.push(Integer.parseInt(parts[index]));
            }

            index++;
        }

        return numbers.pop();
    }

    private boolean isOperation(String part) {
        return part.equals("+")
                || part.equals("-")
                || part.equals("*");
    }
}
```
