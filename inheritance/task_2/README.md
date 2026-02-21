# Задача

### Создайте базовый класс Employee и два класса-наследника: FullTimeEmployee и Freelancer.

#### Требования

1. Класс Employee
    - Поля (private):
    - name (String)
    - baseSalary (double)
    - Геттеры и сеттеры.
    - Метод calculateSalary(), который возвращает baseSalary.


2. Класс FullTimeEmployee extends Employee
    - Переопределить метод calculateSalary().
    - Итоговая зарплата = baseSalary + 20000 (фиксированная премия).

3. Класс Freelancer extends Employee
    - Добавить поле:
    - hoursWorked (int)
    - Геттер и сеттер для hoursWorked.
    - Переопределить calculateSalary():
    - Итоговая зарплата = baseSalary * hoursWorked

4. Класс Main
    - Создать объекты через new (без конструкторов).
    - Заполнить данные через сеттеры.
    - Вызвать calculateSalary() у каждого.
    - Вывести результат.

**Пример ожидаемого вывода**

```
FullTimeEmployee salary: 220000.0
Freelancer salary: 80000.0
```

