#java #collections
### Основные понятия

`Iterable` — это интерфейс в `Java`, который определяет контракт для объектов, способных возвращать итератор. Итератор, в свою очередь, позволяет перебирать элементы коллекции или других данных последовательно.
### Применение:

 >[! ] Содержит единственный метод - `Iterator<T> iterator();`. Метод `iterator()` возвращает объект типа `Iterator<T>`, который используется для перебора элементов. `<T>` - это параметр типа, который указывает, какой тип элементов будет итерироваться.

#### Интерфейс `java.util.Iterator<T>`

    - Определяет методы для итерации по коллекции:
        - `boolean hasNext()`: Возвращает `true`, если есть следующий элемент, иначе `false`.
        - `T next()`: Возвращает следующий элемент в коллекции.
        - `void remove()`: Удаляет текущий элемент из коллекции (не обязателен к реализации).

#### Цикл `for-each`:

- Цикл `for-each` является удобным способом перебора элементов коллекции, реализующей интерфейс `Iterable`.
- Синтаксис:
    ```java
    for (T element : iterableObject) {
        // Обработка элемента
    }
    ```
### Примеры использования:

```java
public class CarHashSet implements CarSet {  
    private static final int INITIAL_CAPACITY = 16;  
    private static final double LOAD_FACTOR = 0.75;  
    private int size = 0;  
    private Entry[] array = new Entry[INITIAL_CAPACITY];  

@Override  
    public Iterator<Car> iterator() {  
        return new Iterator<Car>() {  
            int index = 0;  
            int arrayIndex = 0;  
            Entry entry;  
  
            @Override  
            public boolean hasNext() {  
                return index < size;  
            }  
  
            @Override  
            public Car next() {  
                while (array[arrayIndex] == null) {  
                    arrayIndex++;  
                }  
                if (entry == null) {  
                    entry = array[arrayIndex];  
                }  
                Car result = entry.element;  
                entry = entry.next;  
                if (entry == null) {  
                    arrayIndex++;  
                }  
                index++;  
                return result;  
            }  
        };  
    }  
    @Override  
    public boolean add(Car car) {  
        if (size >= (array.length * LOAD_FACTOR)) {  
            increaseArray();  
        }  
        boolean resultAdded = add(car, array);  
        if (resultAdded) {  
            size++;  
        }  
        return resultAdded;  
    }  
    private boolean add(Car car, Entry[] destination) {  
        int position = getElementPosition(car, destination.length);  
        if (destination[position] == null) {  
            Entry entry = new Entry(car, null);  
            destination[position] = entry;  
            return true;  
        } else {  
            // если в массиве уже что-то лежит, то нужно проверить, не совпадает ли этот элемент с нашим объектом  
            // т.е возможно пытаемся добавить дубликат            Entry existendElement = destination[position];  
            while (true) {  
                if (existendElement.element.equals(car)) {  
                    return false; // не добавляем элемент  
                } else if (existendElement.next == null) {  
                    existendElement.next = new Entry(car, null);  
                    return true;  
                } else {  
                    existendElement = existendElement.next;  
                }  
            }  
        }  
    }  
    @Override  
    public boolean remove(Car car) {  
        int position = getElementPosition(car, array.length);  
        if (array[position] == null) {  
            return false;  
        }  
        // находим предпоследний элемент  
        Entry secondLast = array[position];  
        // находим последний элемент  
        Entry last = secondLast.next;  
  
        if (secondLast.element.equals(car)) {  
            array[position] = last;  
            size--;  
            return true;  
        }  
        // делать это нужно до тех пор, пока last != null  
        while (last != null) {  
            if (last.element.equals(car)) {  
                // проверяем, совпадает ли значение последнего элемента  
                secondLast.next = last.next;  
                size--;  
                return true;  
            } else {  
                secondLast = last;  
                last = last.next;  
            }  
        }  
        return false;  
    }  
    @Override  
    public int size() {  
        return size;  
    }  
    @Override  
    public void clear() {  
        array = new Entry[INITIAL_CAPACITY];  
        size = 0;  
    }  
    @Override  
    public boolean contains(Car car) {  
        if (car == null) {  
            return false;  
        }  
        int position = getElementPosition(car, array.length);  
        if (array[position] == null) {  
            return false;  
        }  
        Entry existendElement = array[position];  
        while (true) {  
            if (existendElement.element.equals(car)) {  
                return true;  
            } else if (existendElement.next == null) {  
                return false;  
            } else {  
                existendElement = existendElement.next;  
            }  
        }  
    }  
    private void increaseArray() {  
        Entry[] newArray = new Entry[array.length * 2];  
        for (Entry entry : array) {  
            Entry existsElement = entry;  
            while (existsElement != null) {  
                add(existsElement.element, newArray);  
                existsElement = existsElement.next;  
            }  
        }  
        array = newArray;  
    }  
    private int getElementPosition(Car car, int arrLength) {  
        return Math.abs(car.hashCode() % arrLength); // возвращаем абсолютное значение числа, если значение выйдет отрицательным  
    }    
    private static class Entry {  
        private Car element;  
        private Entry next;  
  
        public Entry(Car element, Entry next) {  
            this.element = element;  
            this.next = next;  
        }  
    }  
}
```

