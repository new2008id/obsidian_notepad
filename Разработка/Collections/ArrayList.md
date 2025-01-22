### Основные понятия

В основе [[ArrayList]] лежит обычный массив. Сама коллекция [[ArrayList]] это просто надстройка над обычным массивом. [[ArrayList]] реализует `interface` - `List`  
### Примеры использования:

Сейчас веду разработка небольшого проекта по работе с машинами. Для примера, у меня реализован `interface` [[CarList]], а после я реализовал методы данного `interface`
```java
public class CarArrayList implements CarList {  
  
    private Car[] array = new Car[10];  
    private int size = 0;  
  
    @Override  
    public Car get(int index) {  
        checkIndex(index);  
        return array[index];  
    }  
  
    @Override  
    public void add(Car car) {  
        if (size >= array.length) {  
            array = Arrays.copyOf(array, array.length * 2);  
//            Car[] newArray = new Car[arrayList.length * 2];  
//            for (int i = 0; i < arrayList.length; i++) {  
//                newArray[i] = arrayList[i];  
//            }  
//            arrayList = newArray;  
        }  
        array[size] = car;  
        size++;  
    }  
  
    @Override  
    public boolean remove(Car car) {  
        for (int i = 0; i < size; i++) {  
            if (array[i].equals(car)) {  
                return removeAt(i);  
            }  
        }  
        return false;  
    }  
  
    @Override  
    public boolean removeAt(int index) {  
        checkIndex(index);  
        for (int i = index; i < size - 1; i++) {  
            array[i] = array[i + 1];  
        }  
        size--;  
        return true;  
    }  
  
    @Override  
    public int size() {  
        return size;  
    }  
  
    @Override  
    public void clear() {  
        array = new Car[10];  
        size = 0;  
    }  
  
    private void checkIndex(int index) {  
        if (index < 0 || index >= size) {  
            throw new IndexOutOfBoundsException();  
        }  
    }  
}
```

Для каждого метода были реализованы `JUnit` тесты - [[CarListTest]] 


