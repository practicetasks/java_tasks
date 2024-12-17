# Задача

Универсальный контейнер для истории изменений

Создайте класс `ChangeTracker`, который позволяет отслеживать историю изменений значения любого типа. Этот класс должен
сохранять все предыдущие версии значения и предоставлять возможность отмены изменений (`undo`).

Функции класса:

1. Установить новое значение – добавляет новую версию значения.
2. Получить текущее значение.
3. Отменить последнее изменение (`undo`).
4. Получить количество сохраненных версий.
5. Просмотреть все версии значений.

Пример использования:
```java
public class Main {
    public static void main(String[] args) {
        // Отслеживание изменений для строки
        ChangeTracker<String> tracker = new ChangeTracker<>();
        tracker.set("Version 1");
        tracker.set("Version 2");
        tracker.set("Version 3");

        System.out.println("Текущее значение: " + tracker.getCurrent()); // Version 3

        tracker.undo();
        System.out.println("После отмены: " + tracker.getCurrent()); // Version 2

        tracker.undo();
        System.out.println("После второй отмены: " + tracker.getCurrent()); // Version 1

        System.out.println("Всего версий: " + tracker.getVersionCount()); // 1

        // Просмотр всех версий
        System.out.println("Все версии: " + tracker.getAllVersions()); // [Version 1]
    }
}
```
