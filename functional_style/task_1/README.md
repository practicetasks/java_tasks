# Задача

Перед вами класс `BookEditor`, который обрабатывает текст книги как набор строк. Основной метод этого класса —
`processText(List<String> sourceText)`. Этот метод возвращает преобразованный набор строк, соответствующий правилам
форматирования книг, принятым в издательстве.

Отдельно преобразуется заголовок, отдельно — каждая строка текста. В `BookEditor` хранятся специальные обработчики — за
них отвечают объекты интерфейсов `HeaderDecorator` для форматирования заголовка и `LineProcessor` для строк.

Мы определили реализацию каждого из обработчиков в обычных Java-классах — `ToUpperCaseHeaderDecorator` приводит название
книги к верхнему регистру, а `CapitalizeFirstLetterProcessor` делает первую букву в каждой строке заглавной.

Ваша задача — переписать код с использованием лямбда-функций вместо классов `ToUpperCaseHeaderDecorator` и
`CapitalizeFirstLetterProcessor`, а также добавить новый обработчик строк, который будет добавлять в конец каждой строки
символ переноса строки `\n`.

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class BookEditor {

    private HeaderDecorator headerDecorator;
    private List<LineProcessor> lineProcessors = new ArrayList<>();

    public static void main(String[] args) {
        BookEditor bookEditor = new BookEditor();

        bookEditor.setHeaderDecorator(new ToUpperCaseHeaderDecorator());
        bookEditor.addLineProcessor(new CapitalizeFirstLetterProcessor());

        List<String> content = Arrays.asList(
                "Приключения Java-программиста",
                "История началась рано утром, ",
                "когда программист вышел из дома, ",
                "решив выпить утренний кофе."
        );

        List<String> resultContent = bookEditor.processText(content);
        System.out.println(resultContent);
    }

    public List<String> processText(List<String> sourceText) {
        List<String> resultText = new ArrayList<>();

        String sourceHeader = sourceText.get(0);
        String decoratedHeader = headerDecorator.decorate(sourceHeader);
        resultText.add(decoratedHeader);

        for (int i = 1; i < sourceText.size(); i++) {
            String currentLine = sourceText.get(i);
            for (LineProcessor processor : lineProcessors) {
                currentLine = processor.processLine(currentLine);
            }
            resultText.add(currentLine);
        }

        return resultText;
    }

    public void setHeaderDecorator(HeaderDecorator headerDecorator) {
        this.headerDecorator = headerDecorator;
    }

    public void addLineProcessor(LineProcessor lineProcessor) {
        this.lineProcessors.add(lineProcessor);
    }
}
```

```java
public interface HeaderDecorator {
    String decorate(String header);
}
```

```java
public interface LineProcessor {
    String processLine(String line);
}
```

```java
public class ToUpperCaseHeaderDecorator implements HeaderDecorator {
    @Override
    public String decorate(String header) {
        return header.toUpperCase() + "\n";
    }
}
```

```java
public class CapitalizeFirstLetterProcessor implements LineProcessor {
    @Override
    public String processLine(String line) {
        return line.substring(0, 1).toUpperCase() + line.substring(1);
    }
}
```

<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>

###### подсказки ниже

- Перепишите функции `decorate` и processLine в формате лямбда-функций по
  образцу `(список входных параметров) -> { блок реализации функции }`.
- Создавать лямбда-функции можно в том же месте кода, где сейчас создаются конкретные объекты — реализации
  интерфейсов `ToUpperCaseHeaderDecorator` и `CapitalizeFirstLetterProcessor`.
- Сами классы `ToUpperCaseHeaderDecorator` и `CapitalizeFirstLetterProcessor` вам больше не нужны — их можно удалить.