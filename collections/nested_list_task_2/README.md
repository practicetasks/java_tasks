# Задача: Оценки студентов

Описание задачи:
Вы разрабатываете программу для хранения оценок студентов по различным предметам. Вам необходимо создать структуру данных для хранения оценок и реализовать функциональность для вычисления средней оценки по каждому предмету и общей средней оценки для каждого студента.

Инструкции:
1. Создайте класс `Student` с приватными полями `name` (имя студента) и `grades` (список списков оценок по предметам). Для хранения оценок используйте `List<List<Double>>`.

2. Реализуйте конструктор класса `Student`, который принимает имя студента и инициализирует список оценок.

3. Добавьте метод `addGrades`, который позволит добавлять оценки по каждому предмету в список оценок студента.

4. Реализуйте метод `getAverageGrade`, который вычисляет и возвращает среднюю оценку студента. Для этого пройдитесь по списку оценок и посчитайте сумму всех оценок, а затем разделите эту сумму на количество оценок.

5. Создайте класс `GradeCalculator` (или любое другое название), который будет содержать метод `main`.

6. В методе `main` создайте несколько объектов класса `Student`, используя конструктор и метод `addGrades` для добавления оценок.

7. Создайте список `students` и добавьте туда объекты студентов.

8. Используйте цикл `for-each` для прохода по списку студентов. Внутри цикла:
    - Выведите имя студента.
    - Вложенным циклом проходите по списку оценок для каждого предмета.
    - Вычислите и выведите среднюю оценку для каждого предмета, используя вспомогательный метод `calculateSubjectAverage`.
    - Вызовите метод `getAverageGrade` и выведите общую среднюю оценку студента.

9. Создайте вспомогательный статический метод `calculateSubjectAverage`, который принимает объект студента и индекс предмета в списке оценок. Этот метод должен вычислять и возвращать среднюю оценку для данного предмета.

10. Запустите программу и убедитесь, что средние оценки для каждого предмета и общие средние оценки студентов правильно вычисляются и выводятся на экран.

Следуйте этим шагам, чтобы создать программу, которая позволяет управлять оценками студентов по разным предметам и вычислять средние оценки. По мере решения задачи, убедитесь, что вы понимаете каждый этап и работу каждого метода.
##### Как должна выглядеть программа в main'е
<img width="659" alt="Screenshot 2023-08-31 at 12 02 15" src="https://github.com/practicetasks/java_tasks/assets/122010324/24ec8b8f-5b9f-4aef-a035-19787ad0737a">
