# Задача 1
Исправьте код программы-советчика. Если до зарплаты остаётся меньше 10 дней, сообщения останутся прежними, если же больше 10 — пускай печатается совет для предыдущей категории. Например, если на счету 150_000 тенге и при этом до зарплаты остаётся 17 дней, то напечатается не «Неплохо! Прикупите долларов и зайдите поужинать в классное место.», а «Окей, пора в Макдак!».

```java
double moneyBeforeSalary = 250_000.0; // Количество денег до зарплаты
int daysBeforeSalary = 14;

if (moneyBeforeSalary < 15_000) {
    System.out.println("Сегодня лучше поесть дома. Экономьте, и вы дотянете до зарплаты!");
} else if (moneyBeforeSalary < 50_000) {
    // Здесь нужное условие уже добавили
    if (daysBeforeSalary < 10) {
        System.out.println("Окей, пора в Макдак!");
    } else {
        System.out.println("Сегодня лучше поесть дома. Экономьте, и вы дотянете до зарплаты!");
    }
} else if (moneyBeforeSalary < 150_000) {
    // Допишите условие
    ... {
        System.out.println("Неплохо! Прикупите долларов и зайдите поужинать в классное место.");
    } ... {
        System.out.println("Окей, пора в Макдак!");
    }
} else {
    // Если до зарплаты меньше 10 дней, то едим крабов
    ...
    System.out.println("Класс! Заказывайте крабов!");
    // Иначе — доллары и ужин в хорошем ресторане
    ...
    System.out.println("Неплохо! Прикупите долларов и зайдите поужинать в классное место.");
}
```
