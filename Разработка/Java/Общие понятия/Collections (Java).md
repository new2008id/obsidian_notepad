#collections #java #ArrayList
### Основные понятия

`Коллекции в Java` — это мощный и гибкий фреймворк, предназначенный для работы с группами объектов. Они предоставляют абстракции и интерфейсы для хранения, обработки и управления данными. В отличие от массивов, коллекции могут динамически менять свой размер и предлагают множество готовых методов для работы с данными.

## Примеры использования

```java
ArrayList<Integer> numbers = new ArrayList<>(); // 5 numbers list, 0 in unitil 5  
ArrayList<String> collectionString = new ArrayList<>(); // 1 - name  
ArrayList<String> myNames = getMyArrayList(); // 5 names list  
  
for (int i = 0; i < 5; i++) {  
    numbers.add(i);  
    collectionString.add(numbers.get(i) + " - " + myNames.get(i));  
}  
  
for (String result : collectionString) {  
    System.out.println(result);  
}
```

>[! ] Данный пример иллюстрирует базовое использование `ArrayList` c двумя ссылочными типами - `Integer` и `String`

### Методы для работы с данными
```java 
names.add("Alice"); // добавляет элемент по имени
names.add("Bob");
names.remove("Bob"); // удаляет элемент по имени
numbers.add(1); 
numbers.contains(1); // проверяет содержит ли ArrayList элемент 1 
ages.put("Alice", 30); 
int aliceAge = ages.get("Alice"); // добавляет в Map пару ключ-значение
```
### Основных реализаций коллекций достаточно много:
1. **`ArrayList`**
2. **`LinkedList`**
3. [[HashSet]]
4. **`LinkedHashSet`**
5. **`TreeSet`**
6. **`HashMap`**
7. **`LinkedHashMap`**
8. **`TreeMap`**
9. **`PriorityQueue`**