# Задача

Доработайте код клиента для получения курса валют. Извлеките из ответа сервера текущие курсы евро к
доллару и к тенге. Запишите их в переменные `rateKZT` и `rateUSD` и выведите на экран. Сервер возвращает JSON-данные со
следующей структурой: `{"rates": {"<название_валюты1>": <курс_валюты1>, "название_валюты2": <курс_валюты2>}}`

```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

import com.google.gson.JsonElement;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;

public class Practice {
    public static void main(String[] args) {
        HttpClient client = HttpClient.newHttpClient();

        URI url = URI.create("https://api.apilayer.com/exchangerates_data/latest?base=EUR&symbols=KZT,USD&apikey=iISN69jOgAmSSuWq5GG68tko23CuqMLk");
        HttpRequest request = HttpRequest.newBuilder()
                .uri(url)
                .GET()
                .build();

        try {
            HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
            // проверяем, успешно ли обработан запрос
            if (response.statusCode() == 200) {
                JsonElement jsonElement = JsonParser.parseString(response.body());
                if (!jsonElement.isJsonObject()) { // проверяем, точно ли мы получили JSON-объект
                    System.out.println("Ответ от сервера не соответствует ожидаемому.");
                    return;
                }
                // получите курс тенге и доллара и запишите в переменные rateKZT и rateUSD
                ...

                System.out.println("Стоимость евро в тенге: " + rateKZT + " KZT");
                System.out.println("Стоимость евро в долларах: " + rateUSD + " USD");
            } else {
                System.out.println("Что-то пошло не так. Сервер вернул код состояния: " + response.statusCode());
            }
        } catch (IOException | InterruptedException e) { // обрабатываем ошибки отправки запроса
            System.out.println("Во время выполнения запроса возникла ошибка.\n" +
                    "Проверьте, пожалуйста, адрес и повторите попытку.");
        }
    }
}
```

_подсказки ниже_

<br><br><br><br><br><br><br><br><br><br><br><br>

- Чтобы разобрать строку в формате JSON на элементы, необходимо воспользоваться методом `parseString(String json)`.
- Валюты хранятся внутри JSON-объекта `rates`.
- Названия полей курса тенге и доллара внутри JSON — `KZT` и `USD` соответственно.