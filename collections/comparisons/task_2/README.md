# Задача

В лаборатории высокотехнологичного агрохолдинга разработали уникальную методику селекции картошки. Каждой картофелине из
нового урожая присваивается её уникальный идентификатор, а также измеряются основные характеристики — масса, длина и
ширина. Затем для каждой картофелины вычисляется альфа-характеристика, равная 50% от массы, 65% от длины и 80% от
ширины.

После этого, выбираются две картошки с самым большим показателям альфа-характеристик и две с самым маленьким. Именно они
отправляются на главное испытание, по которому производится вывод, поступит ли этот сорт картошки в продажу или нет.

Вам необходимо реализовать для класса картошки `Potato` интерфейс `Comparable<Potato>`, который сравнит две картофелины
по их альфа-характеристикам.

После этого допишите метод `findPotatoesForExperiment` класса `PotatoLaboratory`, чтобы он находил две самые большие и
две самые маленькие по альфа-характеристикам картошки. Результат выведите в порядке от меньшего к большему.

```java
public class Potato implements Comparable<Potato> {

    public final int id;

    /**
     * Масса
     */
    public final int weight;

    /**
     * Длина
     */
    public final int length;

    /**
     * Ширина
     */
    public final int girth;

    public Potato(int id, int weight, int length, int girth) {
        this.id = id;
        this.weight = weight;
        this.length = length;
        this.girth = girth;
    }

    @Override
    public int compareTo(Potato o) {
        // Сравните картофелины по альфа характеристике
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Potato potato = (Potato) o;
        return id == potato.id;
    }

    @Override
    public int hashCode() {
        return Objects.hash(id);
    }

    @Override
    public String toString() {
        return "Potato{" +
                "id=" + id +
                ", weight=" + weight +
                ", length=" + length +
                ", girth=" + girth +
                '}';
    }
}
```

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class PotatoLaboratory {

    public static void main(String[] args) {
        List<Potato> potatoes = List.of(
                new Potato(1, 30, 30, 30),
                new Potato(2, 35, 31, 35),
                new Potato(3, 40, 35, 44),
                new Potato(4, 28, 44, 41),
                new Potato(5, 33, 23, 30),
                new Potato(6, 35, 33, 33),
                new Potato(7, 38, 41, 24)
        );

        List<Potato> fourUnderExperiment = findPotatoesForExperiment(potatoes);

        System.out.println("Картофелины для эксперимента: " + fourUnderExperiment);
    }

    private static List<Potato> findPotatoesForExperiment(List<Potato> potatoes) {
				/* Вычислите две самые большие и две самые маленькие картофелины, 
           а затем выведите их в порядке от самых маленьких до самых больших.*/
        return null;
    }
}
```

<br><br><br><br><br><br><br><br><br><br>

- Чтобы вычислить альфа-характеристику картофеля, удобно использовать вспомогательный метод `public int calculateAlpha(
  Potato o)`. Его тело будет таким —`{return (int) (o.weight * 0.5 + o.length * 0.65 + o.girth * 0.80);}`.
- Для нахождения минимальной и максимальной картошки можно использовать такой способ: взять сначала минимальный и
  максимальный элемент при помощи методов `Collections.max()` и `Collections.min()`, удалить их из списка, а затем взять ещё
  раз. Помните, что для начала надо сделать изменяемую копию списка при помощи `new ArrayList<>(potatoes)`.
- Есть и второй способ по получению двух максимальных и минимальных элементов. Сначала отсортируйте весь картофель при
  помощи `Collections.sort(...)`, а затем возьмите элементы с правильными индексами.