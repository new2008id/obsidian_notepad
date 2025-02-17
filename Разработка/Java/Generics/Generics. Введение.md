#generics #java 
### Основные понятия

`Generics` (`обобщения`) в `Java` — это механизм, который позволяет параметризовать типы. Это означает, что ты можешь объявить `классы`, `интерфейсы` и `методы`, которые работают с разными типами `данных`, не теряя при этом `типобезопасности`.
### Применение:

```java
public class Box<T> {  
    private T object;  
  
    public Box(T object) {  
        this.object = object;  
    }  
  
    public T getObject() {  
        return object;  
    }  
  
    public void setObject(T object) {  
        this.object = object;  
    }  
}
```

```java
public class Box<K, V, F> {  
    private K key;  
    private V value;  
    private F floatValue;  
  
    public Box(K key, V value, F floatValue) {  
        this.key = key;  
        this.value = value;  
        this.floatValue = floatValue;  
    }  
  
    public K getKey() {  
        return key;  
    }  
  
    public void setKey(K key) {  
        this.key = key;  
    }  
  
    public V getValue() {  
        return value;  
    }  
  
    public void setValue(V value) {  
        this.value = value;  
    }  
  
    public F getFloatValue() {  
        return floatValue;  
    }  
  
    public void setFloatValue(F floatValue) {  
        this.floatValue = floatValue;  
    }   
}
```
### Примеры использования:

```java
Box<Integer> box1 = new Box<>(20);  
Box<Integer> box2 = new Box<>(10);  
box2.setObject("fjdka"); // error  
int n1 = 0;  
int n2 = 0;  
// Также не нужно делать явно преобразование типов  
n1 = box1.getObject();  
n2 = box2.getObject();  
  
 Теперь данную проверку можно не делать, т.к уже точно знаем, что класс принадлежит Integer  
if (box1.getObject() instanceof Integer) {  
    n1 = (int) box1.getObject();  
}  
  
if (box2.getObject() instanceof Integer) {  
    n2 = (int) box2.getObject();  
}  
int expected = 30;  
int result = box1.getObject() + box2.getObject();  
assertEquals(expected, result);
```

```java
Box<String, Integer, Float> box1 = new Box<>("string", 2, 3.5f);  
Box<String, Integer, Float> box2 = new Box<>("string", 5, 6.5f);  
float result1 = box1.getValue() + box1.getFloatValue() + box2.getValue() + box2.getFloatValue();  
int result2 = (int) (box1.getValue() + box1.getFloatValue() + box2.getValue() + box2.getFloatValue());  
  
assertEquals(17, result1);  
assertEquals(17, result2);
```

[[Ограничения на использование Generics типов]]