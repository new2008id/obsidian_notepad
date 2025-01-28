#collections #java 
### Основные понятия

При создании `HashMap` создаётся коллекция на 16 элементов. Когда нужно добавить новый элемент, то определяется хеш-код у ключа, т.к добавляем элементы парами (ключ-значение). Вычисляется позиция ячейки, в которой будут храниться данные объекты.
`add(owner, car1)`

Внутри `HashMap` есть еще один дополнительный класс - Entry, который хранит поля ключа, значения, и ссылки на следующий элемент.

```java
private static class Entry {  
        private CarOwner key;  
        private Car value;  
        private Entry next;  
  
        public Entry(CarOwner key, Car value, Entry next) {  
            this.key = key;  
            this.value = value;  
            this.next = next;  
        }  
    }  
```
### Примеры использования:

```java
public class CarHashMap implements CarMap {  
    private static final int INITIAL_CAPACITY = 16;  
    private static final double LOAD_FACTOR = 0.75;  
    private int size = 0;  
    private Entry[] array = new Entry[INITIAL_CAPACITY];  
  
    @Override  
    public void put(CarOwner key, Car value) {  
        if (key == null) {  
            throw new NullPointerException("Key cannot be null");  
        }  
        if (value == null) {  
            throw new NullPointerException("Value cannot be null");  
        }  
        if (size >= (array.length * LOAD_FACTOR)) {  
            increaseArray();  
        }  
        boolean put = put(key, value, array);  
        if (put) {  
            size++;  
        }  
  
  
    }  
  
    private boolean put(CarOwner key, Car value, Entry[] destination) {  
        int position = getElementPosition(key, destination.length); // вычисляю позицию элемента в массиве  
//        Получите текущий элемент из массива по вычисленной позиции.  
        Entry existedElement = destination[position];  
        if (existedElement == null) {  
            Entry entry = new Entry(key, value, null);  
            destination[position] = entry;  
            return true;  
        } else {  
            while (true) {  
                if (existedElement.key.equals(key)) {  
                    existedElement.value = value;  
                    return false;  
                }  
                if (existedElement.next == null) {  
                    existedElement.next = new Entry(key, value, null);  
                    return true;  
                }  
                existedElement = existedElement.next;  
            }  
        }  
    }  
  
    @Override  
    public Car get(CarOwner key) {  
        if (key == null) {  
            throw new NullPointerException("Key cannot be null");  
        }  
        int position = getElementPosition(key, array.length);  
        Entry existentElement = array[position];  
        if (array[position] == null) {  
            return null;  
        }  
        while (existentElement != null) {  
            if (existentElement.key.equals(key)) {  
                return existentElement.value;  
            }  
            existentElement = existentElement.next;  
        }  
        return null;  
    }  
  
    @Override  
    public Set<CarOwner> keySet() {  
        Set<CarOwner> keySet = new HashSet<>();  
        for (Entry entry : array) {  
            if (entry != null) {  
                Entry current = entry;  
  
                while (current != null) {  
                    keySet.add(current.key);  
                    current = current.next;  
                }  
            }  
        }  
        return keySet;  
  
    }  
  
    @Override  
    public List<Car> values() {  
        List<Car> values = new ArrayList<>();  
        for (Entry entry : array) {  
            if (entry != null) {  
                Entry current = entry;  
                while (current != null) {  
                    values.add(current.value);  
                    current = current.next;  
                }  
            }  
        }  
        return values;  
    }  
  
    @Override  
    public boolean remove(CarOwner key) {  
        if (key == null) {  
            throw new NullPointerException("Key cannot be null");  
        }  
        int position = getElementPosition(key, array.length);  
        Entry existentCurrentElement = array[position];  
        if (existentCurrentElement != null && existentCurrentElement.key.equals(key)) {  
            array[position] = existentCurrentElement.next;  
            size--;  
            return true;  
        } else {  
            while (existentCurrentElement != null) {  
                Entry nextElement = existentCurrentElement.next;  
                if (nextElement == null) {  
                    return false;  
                }  
                if (nextElement.key.equals(key)) {  
                    existentCurrentElement.next = nextElement.next;  
                    size--;  
                    return true;  
                }  
                existentCurrentElement = existentCurrentElement.next;  
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
  
    private int getElementPosition(CarOwner carOwner, int arrayLength) {  
        return Math.abs(carOwner.hashCode() % arrayLength);  
    }  
  
    private void increaseArray() {  
        CarHashMap.Entry[] newArray = new CarHashMap.Entry[array.length * 2];  
        for (Entry entry : array) {  
            Entry existsElement = entry;  
            while (existsElement != null) {  
                put(existsElement.key, existsElement.value, newArray);  
                existsElement = existsElement.next;  
  
//                int newPosition = getElementPosition(existsElement.key, newArray.length);  
//                Entry newEntry = new Entry(existsElement.key, existsElement.value, newArray[newPosition]);  
//                newArray[newPosition] = newEntry;  
//                existsElement = existsElement.next;  
            }  
        }  
        array = newArray;  
    }  
  
    private static class Entry {  
        private CarOwner key;  
        private Car value;  
        private Entry next;  
  
        public Entry(CarOwner key, Car value, Entry next) {  
            this.key = key;  
            this.value = value;  
            this.next = next;  
        }  
    }  
}
```



