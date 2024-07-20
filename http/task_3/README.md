# Задача

Реализуйте API со следующей логикой:

- Для метода GET `/hello` всегда возвращается один ответ — «Здравствуйте!».
- Для метода POST `/hello/{профессия}/{имя}`:
    - Если передан заголовок `X-Wish-Good-Day=true`, возвращается ответ вида «{приветствие}, {профессия} {имя}! Хорошего
      дня!». Например, на запрос `/hello/программист/Абай`, заголовок `wishGoodDay=true` и тело запроса `Доброе утро`
      корректный ответ — «Доброе утро, программист Абай! Хорошего дня!».
    - Если заголовок отсутствует, возвращается ответ вида «{приветствие}, {профессия} {имя}!».
- Для любого другого метода выводится сообщение об ошибке «Некорректный метод!».

Будьте внимательны! При возникновении ошибки (например, `NullPointerException`) в консоли не будет отображаться никакой
информации, поэтому тестируйте аккуратно!

```java
import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;
import com.sun.net.httpserver.HttpServer;

import java.io.IOException;
import java.io.OutputStream;
import java.net.InetSocketAddress;
import java.util.List;

public class Practice {
    private static final int PORT = 8080;

    public static void main(String[] args) throws IOException {
        HttpServer httpServer = HttpServer.create();

        httpServer.bind(new InetSocketAddress(PORT), 0);
        httpServer.createContext("/hello", new HelloHandler());
        httpServer.start();
        System.out.println("HTTP-сервер запущен на " + PORT + " порту!");
    }

    static class HelloHandler implements HttpHandler {
        @Override
        public void handle(HttpExchange httpExchange) throws IOException {
            String response;

            // извлеките метод из запроса
            String method = ...

            switch (...){
                // сформируйте ответ в случае, если был вызван POST-метод
                case ...:
                    // извлеките path из запроса
                    String path = ...
                    // а из path — профессию и имя
                    String profession = ...
                    String name = ...

                    // извлеките заголовок
                    List<String> wishGoodDay = ...

                    // соберите ответ
                    response = ...
                    // не забудьте про ответ для остальных методов
            }

            httpExchange.sendResponseHeaders(200, 0);
            try (OutputStream os = httpExchange.getResponseBody()) {
                os.write(response.getBytes());
            }
        }
    }
}
```

_подсказки ниже_

<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>

- Получить HTTP-метод можно с помощью `httpExchange.getRequestMethod()`.
- Так как нужно тело запроса из одной строки, можно воспользоваться методом `bufferedReader.readLine();`.
- Получить профессию и имя из запроса можно с помощью следующего кода.
    ```java
  String path = httpExchange.getRequestURI().getPath();
  String[] splitStrings = path.split("/");
  String profession = splitStrings[2];
  String name = splitStrings[3];
    ```
- Проверить нужный заголовок поможет этот код.
    ```java
  List<String> wishGoodDay = requestHeaders.get("X-Wish-Good-Day");
  if ((wishGoodDay != null) && (wishGoodDay.contains("true"))) {
      ...
  }
    ```