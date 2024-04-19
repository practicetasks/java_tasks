# Задача

Перед вами часть программы для хранения списка задач с приоритетом. Приоритет (англ. _task priority_) может быть:

- высокий (англ. _high_) — `TaskPriority.HIGH`,
- средний (англ. _medium_) — `TaskPriority.MEDIUM`,
- низкий (англ. _low_) — `TaskPriority.LOW`.
Вам нужно реализовать поиск задач с наивысшим приоритетом из предложенного списка.


##### Task

```java
public class Task {

    ... // добавьте переменную priority с приоритетом задачи
    private String description;

    ...// добавьте конструктор класса

    ... // добавьте метод get для приоритета

    public String getDescription() {
        return description;
    }
}
```


##### main
```java
// импортируйте нужные пакеты

public class Practice {

    public static void main(String[] args) {
        List<Task> tasks = new ArrayList<>();
        tasks.add(new Task(TaskPriority.HIGH, "Оплатить интернет."));
        tasks.add(new Task(TaskPriority.LOW, "Сходить в парикмахерскую."));
        tasks.add(new Task(TaskPriority.MEDIUM, "Выбрать подарок подруге на ДР."));
        tasks.add(new Task(TaskPriority.MEDIUM, "Купить билеты в театр."));
        tasks.add(new Task(TaskPriority.HIGH, "Посетить вебинар по английскому языку."));
        tasks.add(new Task(TaskPriority.LOW, "Купить пылесос."));

        System.out.println("Задачи с наивысшим приоритетом на сегодня:");
        ... // цикл for для поиска задач
    }
}
```

