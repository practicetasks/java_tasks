### Задача: Расчет стоимости аренды автомобиля

##### Цель:

Создать программу, которая рассчитывает стоимость аренды автомобиля, учитывая различные факторы, такие как:
местоположение, класс автомобиля, длительность аренды и дополнительные услуги.

##### Функциональные требования:

1. Ввод данных:
    - Страна и город аренды (`String country`, `String city`)
    - Класс автомобиля (`String carClass`): "Эконом", "Средний", "Бизнес", "Внедорожник"
    - Количество дней аренды (`int days`)
    - Дополнительные услуги:
        - Страховка (`boolean insurance`)
        - Детское кресло (`boolean childSeat`)
2. Расчет стоимости:
    - Базовая стоимость:
        - Метод `calculateBasePrice(String country, String city, String carClass)`:
            - Определяет базовую цену в зависимости от класса автомобиля:
                - "Эконом": 30 у.е./день
                - "Средний": 50 у.е./день
                - "Бизнес": 80 у.е./день
                - "Внедорожник": 100 у.е./день
        - Применяет наценки к базовой цене в зависимости от страны и города:
            - США: +20%
                - Крупные города США (Нью-Йорк, Лос-Анджелес): +10%
            - Германия: +10%
            - Берлин: +5%
        - Возвращает значение базовой стоимости (`double`).
    - Стоимость за дни аренды:
        - Метод `calculateDaysPrice(double basePrice, int days)`:
            - Умножает базовую цену на количество дней аренды.
            - Применяет скидку 10%, если количество дней больше 7.
            - Возвращает стоимость за дни аренды (`double`).
    - Стоимость дополнительных услуг:
        - Метод `calculateExtrasPrice(boolean insurance, boolean childSeat)`:
            - Добавляет стоимость страховки (15 у.е./день), если выбрана.
            - Добавляет стоимость детского кресла (5 у.е./день), если выбрано.
            - Возвращает общую стоимость дополнительных услуг (`double`).
3. Вывод данных:
    - Отображает:
        - Базовую стоимость аренды
        - Стоимость за дни аренды
        - Стоимость дополнительных услуг
        - Итоговую стоимость аренды

**Сценарии:**

- Сценарий 1: Эконом класс в США
    - Вход: "USA", "Chicago", "Эконом", 5 дней, без страховки и детского кресла.
    - Ожидаемый результат: базовая цена с наценками для США и Чикаго, умноженная на 5.
- Сценарий 2: Бизнес класс в Германии с длительной арендой
    - Вход: "Germany", "Munich", "Бизнес", 10 дней, со страховкой.
    - Ожидаемый результат: базовая цена с наценками для Германии, умноженная на 10 с учетом скидки, плюс стоимость
      страховки.
- Сценарий 3: Внедорожник в Лос-Анджелесе с дополнительными услугами
    - Вход: "USA", "Los Angeles", "Внедорожник", 3 дня, со страховкой и детским креслом.
    - Ожидаемый результат: базовая цена с наценками для США и Лос-Анджелеса, умноженная на 3, плюс стоимость страховки и
      детского кресла.