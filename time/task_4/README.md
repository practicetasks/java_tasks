# Задача

В компании ООО «Ретроградный Меркурий» для улучшения планирования решили использовать ретроанализ: определять, сколько
по времени будет выполняться задача, если известно, во сколько она была начата и закончена в прошлый раз. Восстановите
пропущенные участки кода. Воспользуйтесь классом `DateTimeFormatter`, чтобы выводить время в формате `часы:минуты` (
например, `12:34`).


```java
import java.time.Duration;
import java.time.LocalTime;
import java.time.format.DateTimeFormatter;


public class Practice {
    public static void main(String[] args) {
        // время начала работы над задачей — 9:00
        LocalTime taskStart = LocalTime.of(...);
        // время окончания работы над задачей — 11:30
        LocalTime taskFinish = LocalTime.of(...);

        // опишите формат вывода в виде часы:минуты
        DateTimeFormatter formatter = ...

        // найдите продолжительность между двумя единицами времени
        Duration duration = ...
        
        // taskStart должен быть выведен в указанном формате
        System.out.println("В прошлый раз задача была начата в " + ... + ",");
        // taskFinish должен быть выведен в указанном формате
        System.out.println("а закончена в " + ... + ".");
        
        LocalTime now = LocalTime.now();
        // now должен быть выведен в указанном формате
        System.out.println("Сейчас " + ... + ".");

        // прибавьте к текущему моменту вычисленную продолжительность
        LocalTime finishTime = ...;

        // finishTime должен быть выведен в указанном формате
        System.out.println("Значит, задача будет выполнена к " + ... + ".");
    }
}
```