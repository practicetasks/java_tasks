# Задача

У нас есть функция, которая определяет категорию возраста: ребенок, подросток, взрослый или пенсионер.

### Категории возраста:

1. Ребенок: 0-12 лет
2. Подросток: 13-17 лет
3. Взрослый: 18-64 года
4. Пенсионер: 65 лет и старше
5. Если передали число меньше 0, выбрасываете исключение `IllegalArgumentException` с
   сообщением `Возраст не может быть отрицательным`


### Функция для тестирования

```java
public class AgeCategory {
    // Данный метод должен возвращать строку ссылаясь на переданный возраст
    public String getCategory(int age) {

    }
}
```

### Тесты на JUnit

```java
import static org.junit.jupiter.api.Assertions.*;

import org.junit.jupiter.api.Test;

public class AgeCategoryTest {

    private final AgeCategory ageCategory = new AgeCategory();

    // Граничные значения
    @Test
    void testBoundaryChildToTeenager() {
       assertEquals("Ребенок", ageCategory.getCategory(12));
       assertEquals("Подросток", ageCategory.getCategory(13));
    }
    
    ...

    // Классы эквивалентности
    @Test
    void testChildCategory() {
       assertEquals("Ребенок", ageCategory.getCategory(5));
    }
    
    ...
}
```

### Тесты

1. **Граничные значения**:
    - **`testBoundaryChildToTeenager`**: Проверяет переход от категории "Ребенок" к "Подросток" (возраста 12 и 13).
    - **`testBoundaryTeenagerToAdult`**: Проверяет переход от категории "Подросток" к "Взрослый" (возраста 17 и 18).
    - **`testBoundaryAdultToSenior`**: Проверяет переход от категории "Взрослый" к "Пенсионер" (возраста 64 и 65).
    - **`testNegativeAge`**: Проверяет, что отрицательный возраст вызывает исключение.

2. **Классы эквивалентности**:
    - **`testChildCategory`**: Проверяет возраст, попадающий в категорию "Ребенок" (например, 5 лет).
    - **`testTeenagerCategory`**: Проверяет возраст, попадающий в категорию "Подросток" (например, 15 лет).
    - **`testAdultCategory`**: Проверяет возраст, попадающий в категорию "Взрослый" (например, 30 лет).
    - **`testSeniorCategory`**: Проверяет возраст, попадающий в категорию "Пенсионер" (например, 70 лет).

