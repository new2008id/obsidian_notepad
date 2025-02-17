#string
### Основные понятия

Метод `toString()` — это метод, объявленный в классе `Object` (базовый класс для всех классов в Java). Он возвращает строковое представление объекта. По умолчанию `toString()` возвращает строку, содержащую имя класса и хэш-код объекта.
### Применение:

- Когда нужно напечатать объект с помощью `System.out.println()`, Java автоматически вызывает метод `toString()` этого объекта.
- Если метод `toString()` не переопределен в классе, используется реализация по умолчанию из класса `Object`.
- Переопределение `toString()` позволяет настраивать представление объектов в виде строк.
### Примеры использования:

```java
public class Person {  
    private String name;  
    private int age;  
  
    public Person(String name, int age) {  
        this.name = name;  
        this.age = age;  
    }  
  
    @Override  
    public String toString() {  
//        return "Name: " + name + ", Age: " + age;  
        return String.format("Name: %s, Age: %d", name, age);  
    }  
}
```

