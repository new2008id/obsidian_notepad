## Общие понятия

Модификатор `abstract` используется для объявления абстрактных классов и методов. Это важный элемент объектно-ориентированного программирования, позволяющий создавать шаблоны классов и определять общий интерфейс для группы связанных классов, предоставляя частичную реализацию.

#### Пример использования

```java
abstract class Shape {
    String color;

    public Shape(String color) {
       this.color = color;
    }
    //Конкретный метод
    public void setColor(String color) {
      this.color = color;
    }
   // Абстрактный метод (без реализации)
    abstract double calculateArea();
    // Абстрактный метод (без реализации)
    abstract double calculatePerimeter();
}
```