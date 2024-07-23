# Задача

Добавьте в код сервера новый обработчик для эндпоинта `/day`. Сервер должен отвечать случайно выбранным днём недели, то
есть одной из строк — `"MON"`, `"TUE"`, `"WED"`, `"THU"`, `"FRI"`, `"SAT"`, `"SUN"`.


```java
import com.sun.net.httpserver.HttpServer;

import java.io.IOException;
import java.net.InetSocketAddress;

public class Practice {
    private static final int PORT = 8080;

    // IOException могут сгенерировать методы create() и bind(...)
    public static void main(String[] args) throws IOException {
        HttpServer httpServer = HttpServer.create();

        httpServer.bind(new InetSocketAddress(PORT), 0);
        httpServer.createContext("/hello", new HelloHandler());
        // добавьте новый обработчик для /day тут
        httpServer.start(); // запускаем сервер

        System.out.println("HTTP-сервер запущен на " + PORT + " порту!");
    }
}
```


```java
import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;

import java.io.IOException;
import java.io.OutputStream;

public class HelloHandler implements HttpHandler {
    @Override
    public void handle(HttpExchange httpExchange) throws IOException {
        System.out.println("Началась обработка /hello запроса от клиента.");

        String response = "Hey! Glad to see you on our server.";
        httpExchange.sendResponseHeaders(200, 0);

        try (OutputStream os = httpExchange.getResponseBody()) {
            os.write(response.getBytes());
        }
    }
}
```