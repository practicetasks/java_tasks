# Задача

Вы практически завершили реализацию HTTP-сервера. Осталось написать обработку эндпоинта для добавления комментариев. Для
этого реализуйте метод `handlePostComments`.

В процессе реализации учтите обработку следующих ситуаций:

- Если комментарий успешно добавлен, то ответ должен содержать текст `Комментарий добавлен`, а его код должен быть равен
  `201`.
- Если был передан некорректный идентификатор поста, то ответ должен содержать текст `Некорректный идентификатор поста`,
  а
  его код должен быть равен `400`.
- Если пост с указанным идентификатором не найден, то ответ должен содержать текст `Пост с идентификатором postId не
  найден`, где вместо `postId` будет переданный идентификатор. Код ответа должен быть равен `404`.
- Если в теле HTTP-запроса был передан синтаксически некорректный JSON, то ответ должен содержать текст `Получен
  некорректный JSON`, а код состояния должен быть равен `400`.
- Если в комментарии не указан текст или пользователь, то ответ должен содержать текст `Поля комментария не могут быть
  пустыми`, а код ответа должен быть равен `400`.

```java
import java.util.ArrayList;
import java.util.List;

public class Post {
    private int id;
    private String text;
    private List<Comment> commentaries = new ArrayList<>();

    private Post() {
    }

    public Post(int id, String text) {
        this.id = id;
        this.text = text;
    }

    public void addComment(Comment comment) {
        commentaries.add(comment);
    }

    public List<Comment> getCommentaries() {
        return commentaries;
    }

    public int getId() {
        return id;
    }
}
```

```java
public class Comment {
    private String user;
    private String text;

    private Comment() {
    }

    public Comment(String user, String text) {
        this.user = user;
        this.text = text;
    }

    public String getUser() {
        return user;
    }

    public String getText() {
        return text;
    }
}
```

```java
public enum Endpoint {
    GET_POSTS,
    GET_COMMENTS,
    POST_COMMENT,
    UNKNOWN
}
```

```java
import com.google.gson.Gson;
import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;

import java.io.IOException;
import java.io.OutputStream;
import java.nio.charset.Charset;
import java.nio.charset.StandardCharsets;
import java.util.ArrayList;
import java.util.List;
import java.util.Optional;

public class PostsHandler implements HttpHandler {
    private static final Charset DEFAULT_CHARSET = StandardCharsets.UTF_8;
    private static final Gson gson = new Gson();
    private static final List<Post> posts = new ArrayList<>();
    
    @Override
    public void handle(HttpExchange exchange) throws IOException {
        Endpoint endpoint = getEndpoint(exchange.getRequestURI().getPath(), exchange.getRequestMethod());

        switch (endpoint) {
            case GET_POSTS: {
                handleGetPosts(exchange);
                break;
            }
            case GET_COMMENTS: {
                handleGetComments(exchange);
                break;
            }
            case POST_COMMENT: {
                handlePostComments(exchange);
                break;
            }
            default:
                writeResponse(exchange, "Такого эндпоинта не существует", 404);
        }
    }

    private void handlePostComments(HttpExchange exchange) throws IOException {
        // реализуйте обработку добавления комментария

        // извлеките идентификатор поста и обработайте исключительные ситуации

        int postId = ...

            /* Получите тело запроса в виде текста в формате JSON и преобразуйте его в объект Comment.
            Учтите, что может быть передан некоректный JSON — эту ситуацию нужно обработать.
            Подумайте, какие ещё ситуации требуют обработки. */
        // ...

        // найдите пост с указанным идентификатором и добавьте в него комментарий
    }

    private Endpoint getEndpoint(String requestPath, String requestMethod) {
        String[] pathParts = requestPath.split("/");

        if (pathParts.length == 2 && pathParts[1].equals("posts")) {
            return Endpoint.GET_POSTS;
        }
        if (pathParts.length == 4 && pathParts[1].equals("posts") && pathParts[3].equals("comments")) {
            if (requestMethod.equals("GET")) {
                return Endpoint.GET_COMMENTS;
            }
            if (requestMethod.equals("POST")) {
                return Endpoint.POST_COMMENT;
            }
        }
        return Endpoint.UNKNOWN;
    }

    private void handleGetPosts(HttpExchange exchange) throws IOException {
        writeResponse(exchange, gson.toJson(posts), 200);
    }

    private void handleGetComments(HttpExchange exchange) throws IOException {
        Optional<Integer> postIdOpt = getPostId(exchange);
        if (postIdOpt.isEmpty()) {
            writeResponse(exchange, "Некорректный идентификатор поста", 400);
            return;
        }
        int postId = postIdOpt.get();

        for (Post post : posts) {
            if (post.getId() == postId) {
                String commentsJson = gson.toJson(post.getCommentaries());
                writeResponse(exchange, commentsJson, 200);
                return;
            }
        }

        writeResponse(exchange, "Пост с идентификатором " + postId + " не найден", 404);
    }

    private Optional<Integer> getPostId(HttpExchange exchange) {
        String[] pathParts = exchange.getRequestURI().getPath().split("/");
        try {
            return Optional.of(Integer.parseInt(pathParts[2]));
        } catch (NumberFormatException exception) {
            return Optional.empty();
        }
    }

    private void writeResponse(HttpExchange exchange,
                               String responseString,
                               int responseCode) throws IOException {
        if (responseString.isBlank()) {
            exchange.sendResponseHeaders(responseCode, 0);
        } else {
            byte[] bytes = responseString.getBytes(DEFAULT_CHARSET);
            exchange.sendResponseHeaders(responseCode, bytes.length);
            try (OutputStream os = exchange.getResponseBody()) {
                os.write(bytes);
            }
        }
        exchange.close();
    }
}
```

```java
import com.sun.net.httpserver.HttpServer;

import java.io.*;
import java.net.InetSocketAddress;

public class Practice {
    private static final int PORT = 8080;

    public static void main(String[] args) throws IOException {
        HttpServer httpServer = HttpServer.create();

        httpServer.bind(new InetSocketAddress(PORT), 0);
        httpServer.createContext("/posts", new PostsHandler());
        httpServer.start(); // запускаем сервер

        System.out.println("HTTP-сервер запущен на " + PORT + " порту!");
    }
}
```

_подсказки ниже_

<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>

- Чтобы получить тело запроса, используйте метод `getRequestBody` класса `HttpExchange`. Он возвращает объект `InputStream`, у
  которого есть метод `readAllBytes`. Используйте его для преобразования тела запроса в строку.
- Чтобы десериализовать JSON в объект класса `Comment`, используйте метод `fromJson` объекта класса `Gson`.
- Если в запросе был передан некорректный JSON, то при его конвертации будет выброшено исключение `JsonSyntaxException`.
  Обработайте его так, как указано в задании.