### Основные понятия

>[! ] Данный интерфейс представлен абстрактную реализацию, которые будут в проекте
### Примеры использования:

```java
public interface CarList {  
    Car get(int index);  
  
    void add(Car car);  
  
    boolean remove(Car car);  
  
    boolean removeAt(int index);  
  
    int size();  
  
    void clear();  
}
```

