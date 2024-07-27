# Задача

Перед вами часть программы, которая представляет в текстовом виде информацию об опубликованных на сайте материалах и
комментариях к ним. Переопределите метод `toString()` у классов `Post` и `PostComment` так, чтобы в консоли появилось
текстовое представление объекта `post`. Формат вывода — тот, который описывается в уроке (в прекоде есть подсказка).
Обратите внимание, что поля обоих классов закрыты модификатором `private` — организуйте к ним доступ с помощью нужных
методов.

```java
public class PostComment {
    private String text; // содержание комментария
    private String[] whoLiked; // кто поддержал
}
```

```java
public class Post {
    private String title; // заголовок
    private String content; // содержание
    private String[] tags; // теги
    private ArrayList<PostComment> comments; //комментарии
 
    /* Вывод должен получиться таким: 
    Post{title='xxx', content.length='x', tags=[x,x], 
    comments=[PostComment{text='x!', whoLiked=[x, x]}, 
    PostComment{text='x', whoLiked=[x,x]}, 
    PostComment{text='x', whoLiked=null}]} */
}
```

```java
import java.util.ArrayList;

public class Practice {
    public static void main(String[] args) {
        Post post = new Post();
        post.setTitle("Почему второй язык программирования выучить проще, чем первый?");
        post.setContent("Если вы научились водить автомобиль на механике, " +
                "вы можете сесть плюс-минус за любой автомобиль и поехать. " +
                "Вам необязательно ездить именно за тем рулём, " +
                "за которым вы учились в автошколе. " +
                "Может быть, первое время вам будет непривычно в новой машине," +
                " но вы быстро освоитесь.");
        post.setTags(new String[]{"Образование", "Карьера в IT"});

        PostComment comment1 = new PostComment();
        comment1.setText("Отличная статья!");
        comment1.setWhoLiked(new String[]{"Asan93", "934Erla1"});

        PostComment comment2 = new PostComment();
        comment2.setText("Тема не раскрыта :(");
        comment2.setWhoLiked(new String[]{"Kuka070707", "Maxa90"});

        PostComment comment3 = new PostComment();
        comment3.setText("❤❤❤");

        ArrayList<PostComment> comments = new ArrayList<>();
        comments.add(comment1);
        comments.add(comment2);
        comments.add(comment3);
        post.setComments(comments);

        System.out.println(post);
    }
}
```

_подсказки ниже :)_

<br><br><br><br><br><br><br><br><br><br><br><br><br>

- Чтобы задать значения полям, закрытыми модификатором `private`, нужно написать `set-` методы.
- У поля `content` нужно вывести не содержание, а длину. Прежде чем это сделать, проверьте, не передана ли в него пустая
  ссылка.
- Получить содержание массива нужно с помощью метода `Arrays.toString()`.
- Чтобы работать с классами `ArrayList` и `Arrays` в классе, их нужно импортировать.