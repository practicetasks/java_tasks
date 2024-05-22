# Задача

Фабрика по производству печенек с предсказаниями развивается. Старый сложный класс разбили на несколько классов, чтобы
каждый из них можно было проще понять и протестировать. Основой нового приложения является класс
`FortuneCookieController`. Он принимает запросы от пользователей и выдаёт печеньки `FortuneCookie`. Печеньки пекутся в
`FortuneCookieFactory`, которая также принимает параметр конфигурации `FortuneConfig`. Через класс-конфигурацию
предполагается в будущем передать все параметры фабрики, но пока это только флаг, указывающий на тип предсказаний —
позитивные или негативные.

Вам нужно написать всего пять тестов. Два на FortuneCookieController и ещё три на FortuneCookieFactory.
`FortuneCookieControllerTest`:

1. `shouldReturnPositiveFortune` должен проверять, что фабрика может испечь печеньку с хорошим предсказанием.
2. `shouldReturnNegativeFortune` проверит, что фабрика также умеет печь печеньки с негативными предсказаниями.

`FortuneCookieFactoryTest`:

1. `shouldIncrementCountByOneAfterOneCookieBaked` проверит, что счётчик печенек в фабрике увеличивается на единицу после
   одной испечённой печеньки.
2. `shouldIncrementCountByTwoAfterTwoCookiesBaked` проверит, что после двух испечённых печенек счёт увеличится на два.
3. `shouldSetCounterToZeroAfterResetCookieCreatedCall` проверит, что после вызова `resetCookiesCreated` счётчик станет
   равным нулю.

`FortuneCookieControllerTest`:

```java
public class FortuneCookieControllerTest {

}
```

`FortuneCookieFactoryTest`:

```java
public class FortuneCookieFactoryTest {

}
```

```java
public class FortuneCookie {
    private final String fortuneText;

    public FortuneCookie(String fortuneText) {
        this.fortuneText = fortuneText;
    }

    public String getFortuneText() {
        return this.fortuneText;
    }
}
```

```java
/** Хранит конфигурацию фабрики по производству печенек с предсказаниями.*/
public class FortuneConfig {
    private final boolean isPositive;

    public FortuneConfig(boolean isPositive) {
        this.isPositive = isPositive;
    }

    public boolean isPositive() {
        return isPositive;
    }
}
```

```java
import java.util.List;
import java.util.Random;

public class FortuneCookieFactory {

    private final FortuneConfig fortuneConfig;
    private int cookiesBaked = 0;

    private final Random rnd = new Random();
    private final List<String> goodFortune;
    private final List<String> badFortune;

    public FortuneCookieFactory(FortuneConfig fortuneConfig, List<String> goodFortune, List<String> badFortune) {
        this.fortuneConfig = fortuneConfig;
        this.goodFortune = goodFortune;
        this.badFortune = badFortune;
    }

    /**
     * Возвращает количество испечённых печенек
     */
    public int getCookiesBaked() {
        return this.cookiesBaked;
    }

    /**
     * Обнуляет счётчик созданных печенек
     */
    public void resetCookiesCreated() {
        this.cookiesBaked = 0;
    }

    /**
     * Печёт печеньку!
     */
    public FortuneCookie bakeFortuneCookie() {
        final String fortune;

        // Возвращает хорошее или плохое предсказание
        if (this.fortuneConfig.isPositive()) {
            fortune = goodFortune.get(rnd.nextInt(goodFortune.size()));
        } else {
            fortune = badFortune.get(rnd.nextInt(badFortune.size()));
        }
        incrementNumberOfCookiesCreated();
        return new FortuneCookie(fortune);
    }

    /**
     * Увеличивает счётчик испечённых печенек
     */
    private void incrementNumberOfCookiesCreated() {
        this.cookiesBaked++;
    }
}
```

```java
public class FortuneCookieController {

    private final FortuneCookieFactory fortuneCookieFactory;

    public FortuneCookieController(FortuneCookieFactory fortuneCookieFactory) {
        this.fortuneCookieFactory = fortuneCookieFactory;
    }

    public FortuneCookie tellFortune() {
        return this.fortuneCookieFactory.bakeFortuneCookie();
    }
}
```

_подсказки ниже_

<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>


- Если нужно выполнить код до запуска всех тестов, пометьте статический метод тестового класса аннотацией `@BeforeAll`.
  Чтобы выполнить метод перед запуском каждого теста, поставьте над ним `@BeforeEach`.
- `FortuneCookieFactory` в обоих тестах можно создавать одинаково, например:
  ```java
  new FortuneCookieFactory(
          config,
          singletonList("positive"),
          singletonList("negative")
  )
  ```
- В тестовом классе `FortuneCookieControllerTest` воспользуйтесь аннотацией `@BeforeAll`, чтобы создать сразу все
  контроллеры: контроллер для фабрики с позитивными предсказаниями `goodFactoryController` и для фабрики с негативными —
  `badFactoryController`.
- Создание экземпляра `FortuneCookieController` можно обернуть в метод `create(boolean isPositive)`. Аргумент `isPositive`
  можно передавать в вызов конструктора `FortuneConfig`.
- В методе `shouldReturnPositiveFortune` вызовите метод предсказания у «позитивной» фабрики и проверьте, что следующее
  предсказание с текстом `positive`.
- В методе `shouldReturnNegativeFortune` вызовите метод предсказания у «негативной» фабрики и проверьте, что следующее
  предсказание с текстом `negative`.
- В тесте `FortuneCookieFactoryTest` воспользуйтесь аннотацией `@BeforeEach`, чтобы перед каждым тестом создавалась новая
  фабрика.
- В тесте `shouldIncrementCountByOneAfterOneCookieBaked` испеките одну печеньку и проверьте, что количество печенек
  соответствует `1`.
- В тесте `shouldIncrementCountByTwoAfterTwoCookiesBaked` испеките две печеньки и проверьте, что количество печенек
  соответствует `2`.
- В тесте `shouldSetCounterToZeroAfterResetCookieCreatedCall` испеките одну печеньку, проверьте, что количество печенек
  соответствует `1`. После чего сбросьте счётчик и проверьте количество снова — теперь оно должно быть равно `0`.