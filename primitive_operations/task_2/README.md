# Задача
Агрегатор авиабилетов заказал разработку приложения для планирования путешествий. 
Доработайте фрагмент кода, отвечающий за маршрут Астана-Париж. В коде допущен ряд ошибок: где-то неправильно указано 
условие, где-то некорректно использовано отрицание. Исправьте ошибки так, чтобы приложение работало корректно в 
соответствии с техническим заданием.
ТЗ от заказчика:
* Если вводится летний месяц — рекомендуем остаться в Астане.
* Если прямые билеты в Париж дешевле билетов с пересадкой в Лондоне, то советуем лететь напрямую.
* Если билеты с пересадкой в Лондоне дешевле или равны по стоимости прямым билетам в Париж и у путешественника есть
британская виза, то рекомендуем лететь через Лондон.


```java
import java.util.Scanner;

public class Practice {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int monthNumber;

        while (true) {
            System.out.println("Когда планируется путешествие? Введите номер месяца от 1 до 12.");
            monthNumber = scanner.nextInt();

            if (monthNumber > 12) { // Инвертируйте условие
                break;
            } else {
                System.out.println("Некорректный номер месяца. Введите ещё раз.");
            }
        }
        String season = getSeasonByNumber(monthNumber);

        ... /* Допишите ветвление, которое будет печатать строку:
            System.out.println("Летом лучше остаться в Астане.");
              и завершать выполнение программы */


        System.out.println("Укажите стоимость прямых билетов из Астаны в Париж:");
        int ticketAstanaParis = scanner.nextInt();
        System.out.println("Укажите стоимость билетов из Астаны в Париж с пересадкой в Лондоне:");
        int ticketAstanaLondonParis = scanner.nextInt();
        System.out.println("У вас есть британская виза?");
        System.out.println("1 - да, виза есть");
        System.out.println("0 - визы нет");
        int britainVisa = scanner.nextInt();


        // В этом ветвлении что-то напутано с условиями - исправьте это
        if (!season.equals("Лето")) { // Перенесите проверку на "Лето" в ветвление выше
            if (!(ticketAstanaLondonParis <= ticketAstanaParis)) {
                if (!(britainVisa == 0)) { // Упростите это условие
                    System.out.println("Летим через Лондон!");
                } else {
                    System.out.println("Летим напрямую в Париж!");
                }
            } else {
                System.out.println("Летим напрямую в Париж!");
            }
        }
    }

    private static String getSeasonByNumber(int monthNumber) {
        // Допишите условия ветвления в виде утверждений
        if (...) {
            return "Зима";
        } else if (...) {
            return "Весна";
        } else if (...) {
            return "Лето";
        } else if (...) {
            return "Осень";
        } else {
            return "Зима";
        }
    }
}
```