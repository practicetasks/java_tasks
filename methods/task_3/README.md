# Задача
Прочитайте код. Сейчас программа анализирует расходы на корм одновременно для двух питомцев: кота Пикселя и хомяка Байта — из-за этого в результатах печати можно запутаться. Декомпозируйте код — разбейте его отдельные методы: `sayHello`, `sayEnjoyMeal`, `findMaxExpense` и findExpensesSum. Методы с приветствием и пожеланием приятного аппетита должны быть типа `void`; методы, касающиеся анализа трат, должны возвращать значение.<br> <br>
У всех методов должны быть параметры. Внутри главного метода `main(String[] args)` должны остаться массивы с тратами, вызов методов и вывод результатов трат. <br><br>
Вызовите методы так, чтобы сначала была напечатана информация про Пикселя, а потом про Байта. Порядок вывода такой: сперва приветствие, затем стоимость самого дорогого корма и общие траты на него и только потом пожелание приятного аппетита.

```java
public class Practice {
    public static void main(String[] args) {
        System.out.println("Привет, Пиксель!");
        System.out.println("Привет, Байт!");

        double[] feedExpensesCat = {500.50, 1270.0, 2590.6, 790.20, 390.0, 890.0, 680.4};
        double[] feedExpensesHamster = {349.50, 739.0, 3413.6, 1219.20, 490.0, 120.0, 923.4};

        double maxFeedExpenseCat = 0;
        for (int i = 0; i < feedExpensesCat.length; i++) {
            if (feedExpensesCat[i] > maxFeedExpenseCat) {
                maxFeedExpenseCat = feedExpensesCat[i];
            }
        }

        System.out.println("Твой самый дорогой корм стоил " + maxFeedExpenseCat);

        double maxFeedExpenseHamster = 0;
        for (int i = 0; i < feedExpensesHamster.length; i++) {
            if (feedExpensesHamster[i] > maxFeedExpenseHamster) {
                maxFeedExpenseHamster = feedExpensesHamster[i];
            }
        }

        System.out.println("Твой самый дорогой корм стоил " + maxFeedExpenseHamster);

        double sumFeedCat = 0;
        for (int i = 0; i < feedExpensesCat.length; i++) {
            sumFeedCat = sumFeedCat + feedExpensesCat[i];
        }

        System.out.println("Всего на корм было потрачено " + sumFeedCat);

        double sumFeedHamster = 0;
        for (int i = 0; i < feedExpensesHamster.length; i++) {
            sumFeedHamster = sumFeedHamster + feedExpensesHamster[i];
        }

        System.out.println("Всего на корм было потрачено " + sumFeedHamster);

        System.out.println("Приятного аппетита, Пиксель!");
        System.out.println("Приятного аппетита, Байт!");
    }
}
```
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>






###### Подсказки
* Нужно объявить четыре метода. Все они будут начинаться со служебных слов `public` и `static`.
* Методы с приветствием и пожеланием приятного аппетита будут иметь тип `void` и содержать один параметр — имя. 
* В коде это будет выглядеть так: `sayHello(String name)` и `sayEnjoyMeal(String name)`. 
* Задача этих методов: напечатать заготовленный текст и имя питомца — его нужно подставить при вызове.
* Методы, касающиеся трат, должны возвращать значение — не забудьте указать его тип `double` перед именем каждого метода.
* В качестве параметров они принимают массивы трат — `double[] expenses`.
* Для возврата значения из методов `findMaxExpense` и `findExpensesSum` используйте оператор `return`.
* Вызов методов `findMaxExpense` и `findExpensesSum` с аргументами-массивами поставьте в main внутрь печати фраз 
* про самый дорогой корм и общую сумму расходов. Это должно выглядеть так: `System.out.println("Твой самый дорогой корм стоил " + findMaxExpense(feedExpensesCat));`.