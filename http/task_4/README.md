# Задача

Вам нужно создать HTTP-сервер для небольшой социальной сети. Сервер сможет обрабатывать запросы к трём эндпоинтам:

- `GET /posts` — для получения списка всех постов;
- `GET /posts/{postId}/comments` — для получения комментариев к посту;
- `POST /posts/{postId}/comments` — для добавления нового комментария к посту.

На первом этапе реализуйте метод `getEndpoint` — он будет анализировать, к какому из трёх перечисленных эндпоинтов был
запрос.

Также реализуйте метод `writeResponse`, который возвращает HTTP-ответ с указанным в коде текстом.

```java
import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;
import com.sun.net.httpserver.HttpServer;

import java.io.*;
import java.net.InetSocketAddress;

public class Practice {
    private static final int PORT = 8080;

    public static void main(String[] args) throws IOException {

        // добавьте код для конфигурирования и запуска сервера
        // ...

        System.out.println("HTTP-сервер запущен на " + PORT + " порту!");
    }

    static class PostsHandler implements HttpHandler {
        @Override
        public void handle(HttpExchange exchange) throws IOException {
            // получите информацию об эндпоинте, к которому был запрос
            Endpoint endpoint = ...

            switch (endpoint) {
                case GET_POSTS: {
                    writeResponse(exchange, "Получен запрос на получение постов", 200);
                    break;
                }
                case GET_COMMENTS: {
                    writeResponse(exchange, "Получен запрос на получение комментариев", 200);
                    break;
                }
                case POST_COMMENT: {
                    writeResponse(exchange, "Получен запрос на добавление комментария", 200);
                    break;
                }
                default:
                    writeResponse(exchange, "Такого эндпоинта не существует", 404);
            }
        }

        private Endpoint getEndpoint(String requestPath, String requestMethod) {
            // реализуйте этот метод
            // ...
        }

        private void writeResponse(HttpExchange exchange,
                                   String responseString,
                                   int responseCode) throws IOException {
            /* Реализуйте отправку ответа, который содержит responseString в качестве тела ответа
            и responseCode в качестве кода ответа.
            Учтите, что если responseString — пустая строка, то её не нужно передавать в ответе. */
            // ...
        }

        enum Endpoint {GET_POSTS, GET_COMMENTS, POST_COMMENT, UNKNOWN}
    }
}
```

_подсказки ниже_

<br><br><br><br><br><br><br><br><br><br><br><br><br>

- Чтобы определить, к каким эндпоинтам был сделан запрос, проанализируйте путь, указанный в запросе (
  `exchange.getRequestURI().getPath()`), и HTTP-метод запроса (`exchange.getRequestMethod()`). Эти значения являются
  аргументами метода `getEndpoint`.
- Чтобы отличить эндпоинт получения постов от эндпоинтов, связанных с комментариями, проверьте, заканчивается ли путь на
  `posts` или содержит в себе ещё и `comments`. Также проверьте в пути количество частей, разделённых слешем `/`.
- Чтобы сформировать нужный ответ, получите объект типа `OutputStream` с помощью метода `exchange.getResponseBody()`.
  Обратите внимание: нужно использовать конструкцию `try-with-resources`, чтобы `OutputStream` был закрыт после завершения
  работы с ним.
- Помните: метод `sendResponseHeaders` должен быть вызван до метода `getResponseBody`.
