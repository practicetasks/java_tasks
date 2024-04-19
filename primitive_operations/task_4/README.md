# Задача
Не зря вы столько времени выбирали хомяка — покупка питомца состоялась. Теперь у вас дома живёт Ниндзя, и вы решили 
поучаствовать с ним в конкурсе «Рыжий хомяк года». Но прежде чем это сделать, с помощью кода проверьте, соответствует 
ли Ниндзя условиям конкурса. 

1. Добавьте Ниндзю в массив участников конкурса, учитывая, что он весит 168 грамм, рыже-белый и пушистый, ему уже 3 месяца,
он не побеждал раньше в конкурсах для хомяков.
2. Проверьте, пройдёт ли Ниндзя отбор, учитывая, что к конкурсу допускаются:
   * Хомяки с рыжим окрасом;
   * Хомяки с рыже-белым окрасом, но только если они пушистые;
   * Хомяки с весом от 150 до 200 грамм. Если хомяк пушистый, то вес не имеет значения;
   * Хомяки возрастом 2 месяца и старше;
   * Хомяки, не выигрывавшие раньше этот конкурс.

### Класс Hamster
```java
public class Hamster {
    String name;      // Имя
    double weight;    // Вес
    int age;          // Возраст
    String color;     // Цвет
    boolean isFluffy; // Пушистый
    boolean isWinner; // Победитель прошлых конкурсов

    public Hamster(
            String hamsterName,
            double hamsterWeight,
            int hamsterAge,
            String hamsterColor,
            boolean isFluffyHamster,
            boolean isWinnerHamster
    ) {
        name = hamsterName;
        weight = hamsterWeight;
        age = hamsterAge;
        color = hamsterColor;
        isFluffy = isFluffyHamster;
        isWinner = isWinnerHamster;
    }
}
```

### main
```java
public class Practice {
    public static void main(String[] args) {
        Hamster[] hamsters = new Hamster[]{
                new Hamster("Пушок", 150.5, 2, "Белый", true, false),
                new Hamster("Корочка", 120, 3, "Рыжий", false, false),
                new Hamster("Шалун", 199.9, 4, "Чёрный", false, false),
                new Hamster("Снежинка", 175.9, 4, "Рыжий", false, false),
                new Hamster("Штучка", 199.9, 7, "Чёрный", true, true),
                new Hamster("Баранка", 173.8, 5, "Рыже-белый", true, false),
                ... // Добавьте Ниндзю
        };

        System.out.println("В конкурсе «Рыжий хомяк года» смогут участвовать:");
        for (int i = 0; i < hamsters.length; i++) {
            Hamster hamster = hamsters[i];
            
            // Составьте условие отбора с помощью дополнительных переменных
            boolean isColor = ...
            boolean isWeight = ...
            boolean isAge = ...
       
            if (...) { 
                System.out.println(" - " + hamster.name);
            }
        }
    }
}
```
