# Задача

Доработайте программу. Выведите информацию об IP-адресе `213.186.33.69`. Дополнительно выведите следующие поля:

- `longitude` — долгота;
- `country_neighbours` — соседние страны;
- `country_phone` — телефонный код страны.

В качестве языка локализации укажите французский (`fr`).

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

        // сформируйте правильный URL-адрес
        URI url = URI.create( ... );
        HttpRequest request = HttpRequest.newBuilder()
                .uri(url)
                .GET()
                .build();

        try {
            HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
            // проверяем, успешно ли обработан запрос
            if (response.statusCode() == 200) {
                // передаем парсеру тело ответа в виде строки, содержащей данные в формате JSON
                JsonElement jsonElement = JsonParser.parseString(response.body());
                if (!jsonElement.isJsonObject()) { // проверяем, точно ли мы получили JSON-объект
                    System.out.println("Ответ от сервера не соответствует ожидаемому.");
                    return;
                }
                // преобразуем результат разбора текста в JSON-объект
                JsonObject jsonObject = jsonElement.getAsJsonObject();

                // получаем название страны
                String country = jsonObject.get("country").getAsString();
                // получаем название города
                String city = jsonObject.get("city").getAsString();
                // получаем значение широты
                double latitude = jsonObject.get("latitude").getAsDouble();

                // получите значения полей из задания
                double longitude = ...
                String countryNeighbours = ...
                int countryPhone = ...

                System.out.println("Страна: " + country);
                System.out.println("Город: " + city);
                System.out.println("Широта: " + latitude);
                System.out.println("Долгота: " + longitude);
                System.out.println("Соседние страны: " + countryNeighbours);
                System.out.println("Телефонный код страны: " + countryPhone);
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

- Для получения значения поля воспользуйтесь методом `get(String memberName)`.
- Для преобразования `JsonElement` в строковое значение используйте метод `getAsString()`, а в
  числовое — `getAsDouble()` или `getAsInt()`.