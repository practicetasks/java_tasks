# Задача

Класс `Cake` — часть кондитерского приложения по учёту и продаже тортов. У каждого торта есть название, цена за килограмм
и вес оставшейся части в граммах. Также есть метод `getPiecePrice` для определения приблизительной цены за кусочек торта и
метод `cutPiece` для вычисления веса оставшейся части.

Найдите в коде переменные, которые не меняются и их можно объявить с модификатором `final`.

```java
public class Cake {

    private String name;
    private double weightInGrams;
    private double pricePerKg;

    public Cake(String name, double weightInGrams, double pricePerKg) {
        this.name = name;
        this.weightInGrams = weightInGrams;
        this.pricePerKg = pricePerKg;

        System.out.println("Готов новый торт: " + name);
    }

    // узнать цену кусочка по его весу:
    public void getPiecePrice(double pieceWeight) {
        double price = (pricePerKg / 5000) * pieceWeight;

        System.out.println("Цена за этот кусочек: " + price + " тенге.");
    }

    // определяет, достаточно ли торта для покупки; и если да, то уменьшает вес:
    public void cutPiece(double pieceWeight) {
        if (weightInGrams == 0) {
            System.out.println("К сожалению, этот торт уже закончился.");
        }
        if (weightInGrams < pieceWeight) {
            System.out.println("Пожалуйста, выберите кусочек поменьше.");
        }

        weightInGrams = weightInGrams - pieceWeight;

        System.out.println("Приятного аппетита!");
    }

}
```