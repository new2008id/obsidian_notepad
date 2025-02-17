### Основные понятия

`TreeSet` - это одна из реализаций интерфейса `Set`, которая предоставляет упорядоченное множество элементов. В отличие от `HashSet`, который не гарантирует никакого порядка, `TreeSet` хранит элементы в отсортированном порядке.

>[!warning ] Алгоритмическая сложность - O(Log(N))

>[!success ] Одинакова для всех операций: `add()`, `remove()`, `contains()` 

>[!error ] Общая [[Алгоритмическая сложность в ArrayList]] - `O(1) < O(Log(N)) < O(N)`
### Применение:

**Основные характеристики `TreeSet`:**

1. **Интерфейс `Set`:**
    
    - `TreeSet` реализует интерфейс `java.util.Set`, что означает, что он хранит только уникальные элементы (без дубликатов).
2. **Упорядоченное множество:**
    
    - Элементы в `TreeSet` хранятся в отсортированном порядке.
    - Порядок сортировки определяется либо естественным порядком элементов (если они реализуют интерфейс `Comparable`), либо с помощью `Comparator`, который может быть передан в конструктор `TreeSet`.
3. **Использование дерева:**
    
    - `TreeSet` основан на реализации в виде красно-черного дерева (red-black tree), что обеспечивает логарифмическую сложность для основных операций (добавление, удаление, поиск) - O(log n).
4. **Уникальность элементов:**
    
    - Как и все реализации `Set`, `TreeSet` не допускает дубликатов элементов. Если вы пытаетесь добавить элемент, который уже существует, то он не будет добавлен (дубликаты игнорируются).
5. **`null` элементы:**
    
    - `TreeSet` не допускает хранение `null` элементов, так как `null` нельзя сравнить. При попытке добавить `null` будет выброшено исключение `NullPointerException`.
6. **Производительность:**
    
    - Операции добавления, удаления и поиска имеют логарифмическую сложность O(log n), что делает `TreeSet` хорошим выбором, когда важна производительность и упорядоченное хранение.
    - Потребление памяти чуть больше чем у `HashSet`, из-за хранения информации о структуре дерева.


### Сходства и различия HashSet и TreeSet

#### Сходства
1. Реализуют интерфейс Set;
2. Не хранят повторяющихся элементов.

#### Отличия
1. [[TreeSet]] хранит объекты в отсортированном виде
2. [[HashSet]] может хранить объекты любых классов, а [[TreeSet]] только тех, которые реализуют интерфейс `Comparable`, либо любых классов при условии, что в качестве параметра в конструктор был передан `Comparable`.

>[!success ] Алгоритмическая сложность операций вставки, удаления, и поиска элемента: `HashSet - O(1)`, `TreeSet - O(Log(N))`
### Примеры использования:

```java
public class Car implements Comparable<Car> { // удалил Comparable  
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
    @Override  
    public int compareTo(Car o) {  
//         сравнение по номерам  
        if (number < o.number) {  
            return 1;  
        } else if (number > o.number) {  
            return -1;  
        } else {  
            return 0;  
        }  
  
        // сравнение по brand  
//        return brand.compareTo(o.brand);  
    }  
    @Override  
    public String toString() {  
        return "Car{" +  
                "brand='" + brand + '\'' +  
                ", number=" + number +  
                '}';  
    }  
}
```

```java
public class Main {  
    public static void main(String[] args) {  
        Set<Integer> numbers = new TreeSet<>(new Comparator<Integer>() {  
            @Override  
            public int compare(Integer o1, Integer o2) {  
//                 в порядке убывания  
//                return o2 - o1;  
                return -o1.compareTo(o2);  
                // в порядке возрастания  
//                return o1 - o2;  
            }  
        });  
        for (int i = 0; i < 100; i++) {  
            numbers.add((int) (Math.random() * 10));  
        }  
        for (int number : numbers) {  
            System.out.println(number);  
        }  
    }  
}
```

Здесь используется объект [[Анонимные классы]], реализующий `interface Comparator`