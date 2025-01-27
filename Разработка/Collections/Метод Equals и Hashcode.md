#collections 
### Основные понятия

`equals()` и `hashCode()` — это фундаментальные методы в Java, которые играют ключевую роль при сравнении объектов и использовании коллекций, основанных на хешировании (например, `HashMap`, `HashSet`).

### Применение:

Метод `equals()` используется для сравнения двух объектов на _логическое равенство_. Это означает, что два объекта считаются “равными”, если они представляют одно и то же значение или состояние.
- Метод принимает на вход объект типа `Object`.
- Возвращает `true`, если объекты считаются равными, и `false` в противном случае.

Метод `hashCode()` используется для получения _хеш-кода_ объекта. Хеш-код — это целое число, которое используется для быстрого поиска объекта в хеш-таблицах (например, в `HashMap` и `HashSet`).
- Метод не принимает параметров.
- Возвращает целое число (хеш-код).

### Важность `equals()` и `hashCode()`:

- **Сравнение объектов:** `equals()` позволяет правильно сравнивать объекты на логическое равенство.
- **Коллекции:** `HashMap` и `HashSet` используют `hashCode()` для быстрого поиска объектов. Если ты не переопределишь `hashCode()`, то объекты будут работать неправильно в этих коллекциях.

Здесь описаны [[Правила, для методов equals() и hashCode()]]

### Примеры использования:

```java
public class Car {  
    private final String brand;  
    private int number;  
  
    public Car(String brand, int number) {  
        this.brand = brand;  
        this.number = number;  
    }  
  
    public String getBrand() {  
        return brand;  
    }  
  
    public int getNumber() {  
        return number;  
    }  
  
    public void setNumber(int number) {  
        this.number = number;  
    }  

// переопределение методов
    @Override  
    public boolean equals(Object o) {  
        if (this == o) return true;  
        if (o == null || getClass() != o.getClass()) return false;  
        Car car = (Car) o;  
        return number == car.number && Objects.equals(brand, car.brand);  
    }  
  
    @Override  
    public int hashCode() {  
        return Objects.hash(brand, number);  
    }  
}

public class Main {  
    public static void main(String[] args) {  
        Car car1 = new Car("Audi", 1);  
        Car car2 = new Car("Audi", 1);  
        System.out.println(car1.equals(car2));  
        System.out.println(car1.hashCode());  
        System.out.println(car2.hashCode());  
    }  
}
```
