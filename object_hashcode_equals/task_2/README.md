# Задача

Перед вами часть кода программы, которая по имени актера находит фильмы, где он сыграл. Вот только сейчас она не
запускается. Исправьте это.

1. Доработайте класс `Movie`. Реализуйте конструктор с параметрами, где задаётся название и год выхода фильма.
   Переопределите методы `equals(Object)` и `hashCode()`.
2. Доработайте класс `Actor`. Реализуйте конструктор с параметрами, где задаётся имя и фамилия актёра. Переопределите
   методы `equals(Object)` и `hashCode()`.

```java
public class Actor {
    String firstName;
    String lastName;
}
```

```java
public class Movie {
    String title; // название фильма
    int releaseYear; // год выхода на экраны

    public String description() { // метод для вывода описания фильма
        return '"' + title + "\" (" + releaseYear + " год)";
    }
}
```

```java
import java.util.ArrayList;
import java.util.HashMap;

public class Practice {
    public static void main(String[] args) {
        // Таблицы для хранения рейтингов фильмов и фильмографии актёров
        HashMap<Actor, ArrayList<Movie>> filmography = new HashMap<>();
        HashMap<Movie, Double> ratings = new HashMap<>();

        Movie pulpFictionMovie = new Movie("Криминальное чтиво", 1994);
        Movie dieHardMovie = new Movie("Крепкий Орешек", 1988);
        ratings.put(pulpFictionMovie, 8.9);
        ratings.put(dieHardMovie, 8.2);

        Actor bWillis = new Actor("Брюс", "Уиллис");

        ArrayList<Movie> actorMovies = new ArrayList<>();
        actorMovies.add(pulpFictionMovie);
        actorMovies.add(dieHardMovie);

        filmography.put(bWillis, actorMovies);

        if (filmography.containsKey(new Actor("Брюс", "Уиллис"))) {
            ArrayList<Movie> foundMovies = filmography.get(new Actor("Брюс", "Уиллис"));
            System.out.println("В фильмографии актёра Б. Уиллис найдены следующие фильмы: ");
            for (Movie movie : foundMovies) {
                if (ratings.containsKey(new Movie(movie.title, movie.releaseYear))) {
                    double rating = ratings.get(movie);
                    System.out.println("Фильм " + movie.description() + " с рейтингом " + rating);
                } else {
                    System.out.println("Что-то пошло не так... Проверьте реализацию equals и hashCode в классе Movie.");
                }
            }
        } else {
            System.out.println("Что-то пошло не так... Проверьте реализацию equals и hashCode в классе Actor.");
        }
    }
}
```

_подсказки ниже :)_

<br><br><br><br><br><br><br><br><br><br><br><br>

- Чтобы создать конструкторы с параметрами, используйте ключевое слово `this`.
- Метод `equals(Object)` после переопределения должен проверять, что сравниваемые объекты равны, ни один не равен пустой
  ссылке, классы и значения полей объектов полностью совпадают.
- Для переопределения `hashCode()` воспользуйтесь методом вспомогательного класса `Objects`.
- Чтобы использовать методы `Objects.equals(Object, Object)` и `Objects.hash(Object...)`, нужно импортировать
  класс `Objects`.
- Поля в `equals(Object)` и `hashCode()` должны совпадать.