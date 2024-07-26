# Задача

Частный университет решил автоматизировать процесс завершения студентами обучения. Для студентов, которые не планируют
дальше учиться, выполняются следующие действия:

- Проверяется, сдал ли студент экзамен.
- Указывается группа, где учился студент (на основе года начала обучения).
- В список клуба выпускников добавляется email студента.

Для решения этой задачи используются стрим и лямбда-функции. Ваша задача — реализовать недостающие функции так, чтобы
поддержать логику кода. Обратите внимание — вам придётся использовать механизм замыканий, поскольку список названий
групп и список клуба выпускников, с которыми вам придётся работать в лямбда-функциях, определены в теле метода `main`.

```java
import java.util.*;
import java.util.stream.Collectors;

public class UniversityExample {

    public static void main(String[] args) {
        //множество студентов, успешно сдавших экзамен
        Set<String> examPassedNames = new HashSet<>();
        examPassedNames.add("Иванов Иван");
        examPassedNames.add("Садыков Алибек");

        //соответствие года поступления и названия группы
        Map<Integer, String> groupNames = new HashMap<>();
        groupNames.put(2020, "2020-ГР1");
        groupNames.put(2021, "2021-ГР0");

        //список с адресами email выпускников
        List<String> graduatesClub = new ArrayList<>();

        //студенты, планирующие завершить обучение
        List<Student> students = new ArrayList<>();
        students.add(new Student("Садыков", "Алибек", "asadykov@gmail.com", 2021));
        students.add(new Student("Иванов", "Иван", "ivan_ivanov@gmail.com", 2020));
        students.add(new Student("Аманов", "Куаныш", "iamkuanysh@gmail.com", 2021));

        List<Student> graduatedStudents = students.stream()
                .filter(/* проверка, что студент успешно сдал экзамен */)
                .map(/* заполнение названия группы студента */)
                // операция peek выполняет над элементом действие и передаёт далее тот же элемент
                .peek(/* добавление студента в клуб выпускников */)
                .collect(Collectors.toList());

        for (Student student : graduatedStudents) {
            System.out.println(student);
        }

        for (String email : graduatesClub) {
            System.out.println(email);
        }

    }
}
```

```java
public class Student {
    String surname;
    String name;
    String email;
    int entranceYear;
    String groupName;

    public Student(String surname, String name, String email, int entranceYear) {
        this.surname = surname;
        this.name = name;
        this.email = email;
        this.entranceYear = entranceYear;
    }

    @Override
    public String toString() {
        return "Student{" +
                "surname='" + surname + '\'' +
                ", name='" + name + '\'' +
                ", email='" + email + '\'' +
                ", entranceYear=" + entranceYear +
                ", groupName='" + groupName + '\'' +
                '}';
    }
}
```
###### подсказки ниже

<br><br><br><br><br><br><br><br><br><br>


- Входной параметр у всех лямбд будет одинаковый — `student`.
- Чтобы реализовать каждую из лямбда-функций, вам нужно обратиться к переменным `examPassedNames`, `groupNames`
  и `graduatesClub`.
- В результате операции `map` вместо изначального элемента нужно вернуть результат преобразования.