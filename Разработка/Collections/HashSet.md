#collections #java #ArrayList

`HashMap` - это коллекция, со своими преимуществами.

- Реализация `Map` на основе хеш-таблицы.
- Быстрый поиск, добавление и удаление пар “ключ-значение”.
- Не сохраняет порядок элементов.
- Хорошо подходит для быстрого доступа к значениям по ключу, когда порядок не важен.
## Примеры использования

```java
HashSet<String> names = getMyArrayList(); 
for (String numberName : names) {  
    System.out.println(numberName);  
}

private static HashSet<String> getMyArrayList() {  
    HashSet<String> names = new HashSet<>();  
    names.add("Denis");  
    names.add("Denis");  
    names.add("Dmitriy");  
    names.add("Oleg");  
    names.add("Dmitriy");  
  
    return names;  
}
```