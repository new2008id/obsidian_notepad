#generics 
### Основные понятия

**`super`** - Используется для ограничения типа параметра, указывая, что этот тип должен быть предком (суперклассом) указанного класса или интерфейса.
- **Синтаксис:** `<T super SomeClass>`, `<T super SomeInterface>`.

### Примеры использования:
```java
    public class SomeClass {
    }
    public class SomeChildClass extends SomeClass {

    }
    public void addFruits(Basket<? super SomeChildClass> basket, SomeChildClass fruit){
        basket.add(fruit); //Можно добавлять SomeChildClass или его подтипы
    }
```

```java
public class Basket<T extends Fruit> {  
    private final List<T> fruits;  
  
    public Basket() {  
        this.fruits = new ArrayList<>();  
    }  
  
    public float getWeight() {  
        float weight = 0;  
        for (T item : fruits) {  
            weight += item.getWeight();  
        }  
        return weight;  
    }  
  
    public void add(T item) {  
        fruits.add(item);  
    }  
  
    public int compare(Basket<?> other) {  
        if (other == null) {  
            throw new NullPointerException("Корзина не может быть null");  
        }  
        return Double.compare(getWeight(), other.getWeight());  
    }  
  
//    public static <U> void transfer(List<? extends U> src, List<? super U> dst) {  
//        dst.addAll(src);  
//        src.clear();  
//    }  
  
    public static <U extends Fruit> void transfer(Basket<? extends U> src, Basket<? super U> dst) {  
        dst.fruits.addAll(src.fruits);  
        src.fruits.clear();  
    }  
}
```
