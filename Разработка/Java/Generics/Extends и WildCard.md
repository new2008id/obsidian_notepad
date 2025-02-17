#generics 
### Основные понятия

Можно ограничить типы, которые могут использоваться в качестве параметров типa. 
В этом примере `T extends Number` означает, что в качестве параметра типа `T` можно использовать только классы, которые наследуют класс `Number` (например, `Integer`, `Double`).

>[!warning ] Ключевое слово `extends` в параметризованном классе указывает на то, что можем использовать только тот класс, который используется справа, либо его наследников.

>[! ] Наследоваться можно лишь от `одного` класса, но `интерфейсов`, может быть `много`.

>[!success ] Если нужно `добавить`, чтобы `наследование` было не только от одного класса, но и еще реализовывал определенные `интерфейсы`, то их можно передать через символ `&`

```java
public class NumberBox<T extends Number & Comparable<T> & Serializable> {  
    private T value;  
  
    public NumberBox(T value) {  
        this.value = value;  
    }  
  
    public T getValue() {  
        return value;  
    }  
}
```

>[!error ] Если нужно, чтобы `класс` представлял любой `тип` можно использовать `?` - **неограниченный подстановочный знак**. `<? extends SomeClass>` - ограничение (или `расширение`) типа параметров у `метода`

### Примеры использования:

```java
Box<Integer> box1 = new Box<>(5, 10, 15);  
Box<Float> box2 = new Box<>(5f, 10f, 15f);  
assertEquals(10.0, box1.average(), 0.001);  
assertEquals(0, box1.compare(box2));


public class Box<T extends Number & Comparable<T> & Serializable> {  
    private T[] array;  
    public Box(T... array) {  
        this.array = array;  
    }  
    public T[] getArray() {  
        return array;  
    }  
    public void setArray(T[] array) {  
        this.array = array;  
    }  
    
    public int compare(Box<?> another) {  
        if (average() > another.average()) {  
            return 1;  
        } else if (average() == another.average()) {  
            return 0;  
        } else {  
            return -1;  
        }  
    }  
  
    public double average() {  
        double result = 0;  
        for (T element : array) {  
            result += ((Number) element).doubleValue();  
        }  
        return result / array.length;  
    }  
}
```



