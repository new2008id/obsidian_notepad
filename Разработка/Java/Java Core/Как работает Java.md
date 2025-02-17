#java #interface 
### Основные понятия

[[Отличие интерфейсов и абстрактных классов]]
### Примеры использования:

```java
@FunctionalInterface  
public interface Car extends Serializable {  
    public static final int SPEED = 10;  //public static final можно не указывать
  
    void go();  
  
    default void stop() {  // реализация по умолчанию
        System.out.println("Stopping...");  
    }  
  
    static void printSpeed() {  
        System.out.println("Speed: " + SPEED);  
    }  
}

public class Main {  
    public static void main(String[] args) {  
        Car car = () -> System.out.println("Car running...");  
        car.go();  
        Car.printSpeed();  
    }  
}
```


