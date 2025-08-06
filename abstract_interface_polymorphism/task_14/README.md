# Задача с полиморфизмом - Музыкальные инструменты

1. Создайте абстрактный класс Instrument
    - поля:
        - name (String) - название инструмента
        - volume (int) - громкость от 1 до 10
    - конструктор должен принимать на вход name и volume
    - методы:
        - abstract void play(String melody) - исполнить мелодию
        - void tune() - настроить инструмент (выводит "Настраиваем <name>")

2. Создайте подкласс Piano
    - дополнительное поле:
        - keys (int) - количество клавиш (по умолчанию 88)
    - конструктор принимает name, volume и keys
    - переопределите метод play:
      ```
      Играем мелодию "<melody>" на пианино <name> с громкостью <volume> используя <keys> клавиш
      ```

3. Создайте подкласс Guitar
    - дополнительное поле:
        - strings (int) - количество струн (по умолчанию 6)
    - конструктор принимает name, volume и strings
    - переопределите метод play:
      ```
      Исполняем "<melody>" на гитаре <name> с громкостью <volume> на <strings> струнах
      ```

4. Создайте подкласс Drums
    - дополнительное поле:
        - pieces (int) - количество элементов барабанной установки
    - конструктор принимает name, volume и pieces
    - переопределите метод play:
      ```
      Барабаним ритм "<melody>" на установке <name> с громкостью <volume> используя <pieces> элементов
      ```

## main
```java
public static void main(String[] args) {
    String song = "Happy Birthday";
    
    Instrument[] orchestra = {
            new Piano("Steinway", 7, 88),
            new Guitar("Fender", 5, 6),
            new Drums("Pearl", 8, 5)
    };
    
    // Сначала все настраиваются
    for (Instrument instrument : orchestra) {
        instrument.tune();
    }
    
    System.out.println("--- Начинаем концерт ---");
    
    // Затем играют мелодию
    for (Instrument instrument : orchestra) {
        instrument.play(song);
    }
}
```

## Ожидаемый вывод:
```
Настраиваем Steinway
Настраиваем Fender
Настраиваем Pearl
--- Начинаем концерт ---
Играем мелодию "Happy Birthday" на пианино Steinway с громкостью 7 используя 88 клавиш
Исполняем "Happy Birthday" на гитаре Fender с громкостью 5 на 6 струнах
Барабаним ритм "Happy Birthday" на установке Pearl с громкостью 8 используя 5 элементов
```