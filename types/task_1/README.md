# Задача 
Доработайте код программы, которая анализирует погоду за месяц и определяет, был ли он дождливым. Сейчас поля класса `WeatherCalendar` инициализируются некорректно. Исправьте это. Вы должны учесть, что:
* Значения полей `month` и `numberOfDays` должны присваиваться в конструкторе. Для этого объявите его с двумя параметрами — `monthName` и `monthNumberOfDays`, а при вызове передайте в качестве аргументов значения «Октябрь» и «31».
* Полям `rainyDays` и `isRainyMonth` должны присваиваться значения по умолчанию (сейчас они инициализируются явно).
* Поле `year` должно быть проинициализировано при объявлении на уровне класса. Сохраните в него значение 2023.

Кроме того, внутри `WeatherCalendar` допишите метод `addRainyDay()` — он увеличивает переменную `rainyDays` на единицу. Также нужно дописать код условных выражений. Если дождливых дней в месяце больше 15, необходимо присвоить переменной `isRainyMonth` значение `true`. Чтобы напечатать сообщение-вывод, нужно обратиться к этой переменной.

```java
public class WeatherCalendar {
    String month;
    int numberOfDays;
    int rainyDays;
    int year;
    boolean isRainyMonth;

    // Увеличить переменную rainyDays на единицу
    public void addRainyDay() {
        ...
    }
}
```

```java
public class Practice {
    public static void main(String[] args) {
        WeatherCalendar calendar;
        calendar.month = "Октябрь";
        calendar.numberOfDays = 31;
        calendar.rainyDays = 0;
        calendar.isRainyMonth = false;

        String[] octoberWeather = new String[]{
                "Солнечно",
                "Дождь",
                "Пасмурно",
                "Дождь",
                "Дождь",
                "Облачно",
                "Солнечно",
                "Дождь",
                "Пасмурно",
                "Солнечно",
                "Солнечно",
                "Облачно",
                "Солнечно",
                "Дождь",
                "Пасмурно",
                "Солнечно",
                "Солнечно",
                "Облачно",
                "Облачно",
                "Облачно",
                "Облачно",
                "Дождь",
                "Дождь",
                "Облачно",
                "Солнечно",
                "Дождь",
                "Пасмурно",
                "Дождь",
                "Солнечно",
                "Солнечно",
                "Солнечно",
                "Солнечно",
                "Облачно"
        };

        for (int i = 0; i < calendar.numberOfDays; i++) {
            if (octoberWeather[i].equals("Дождь")) {
                calendar.addRainyDay();
            }
        }

        // Проверить, был ли месяц дождливым. Если да - установить значение isRainyMonth
        if (...){
            ...
        }

        System.out.println(calendar.month + " " + calendar.year + " года. "
                + calendar.rainyDays + " дней шёл дождь.");

        // Проверить значение isRainyMonth
        if (...){
            System.out.println("Это был дождливый месяц.");
        } else{
            System.out.println("Этот месяц был довольно сухим.");
        }
    }
}
```
