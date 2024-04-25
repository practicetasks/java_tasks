# Задача

Онлайн-кинотеатр решил показать своим пользователям, сколько времени они потратили на просмотр фильмов и сериалов на
платформе. У разработчиков есть заготовка программы, которая хранит просмотренные пользователем фильмы `Movie` и сериалы
`Series`. Доработайте её, добавив информацию о том, сколько дней потратил пользователь на просмотр фильмов и сериалов.
Обратите внимание, что их длительность хранится в минутах, а метод должен возвращать длительность в днях.

```java
public interface MediaItem {

    // Длительность фильма или сериала в минутах
    public int getRuntime();

    public String getTitle();

}
```


```java
public class Movie implements MediaItem {

    private final String title;
    private final int runtime;

    public Movie(String title, int runtime) {
        this.title = title;
        this.runtime = runtime;
    }

    @Override
    public int getRuntime() {
        return runtime;
    }

    @Override
    public String getTitle() {
        return title;
    }
}
```

```java
public class Series implements MediaItem {

    private final String title;
    private final int averageRuntime;
    private final int seriesCount;

    public Series(String title, int averageRuntime, int seriesCount) {
        this.title = title;
        this.averageRuntime = averageRuntime;
        this.seriesCount = seriesCount;
    }

    @Override
    public int getRuntime() {
        return averageRuntime;
    }

    @Override
    public String getTitle() {
        return title;
    }

    public int getSeriesCount() {
        return seriesCount;
    }
}
```

```java
import java.util.List;

public class Calculator {

    private Calculator() {}

    public static ... calculate(List<MediaItem> mediaItems) {
        // Напишите реализацию метода, который будет возвращать общее количество дней,
        // потраченных на просмотр фильмов и сериалов
        ...
    }

}
```

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class Practice {

    public static void main(String[] args) {
        List<MediaItem> mediaItems = new ArrayList<>();

        Scanner scanner = new Scanner(System.in);

        while (true) {
            printMenu();
            // Считайте команду, введенную пользователем
            ...

            if (command == 1) {
                System.out.println("Введите название фильма:");
                String title = scanner.next();
                System.out.println("Введите длительность фильма в минутах:");
                int runtime = scanner.nextInt();

                // На основе введенных пользователем значений создайте объект класса Movie
                Movie movie = ...;
                mediaItems.add(movie);
            } else if (command == 2) {
                System.out.println("Введите название сериала:");
                String title = scanner.next();
                System.out.println("Введите количество серий:");
                int seriesCount = scanner.nextInt();
                System.out.println("Введите среднюю длительность серии в минутах");
                int runtime = scanner.nextInt();

                // Создайте сериал и добавьте его в список просмотренных
                ...
            } else if (command == 0) {
                printMediaItemsList(mediaItems);

                double totalRuntime = Calculator.calculate(mediaItems);
                System.out.println("Всего вы потратили на просмотр фильмов и сериалов, в днях: " + totalRuntime);
                break;
            }
        }
    }

    public static void printMenu() {
        System.out.println("1 - Добавить фильм");
        System.out.println("2 - Добавить сериал");
        System.out.println("0 - Посчитать суммарное время и выйти");
    }


    public static void printMediaItemsList(List<MediaItem> mediaItems) {
        System.out.println("Вы посмотрели фильмов и сериалов: " + mediaItems.size());
        // Допишите вывод названий всех просмотренных фильмов и сериалов
        ...
    }

}
```