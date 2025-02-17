#java #stream #ArrayList #collections 
### Основные понятия

1. Метод `stream()` или `parallelStream()` у коллекций. 
2. Статический метод `stream()`у класса `Arrays` для преобразования массива в поток данных.
3. Статические методы класса `Stream` - `of()`, `generate()` и другие.
### Примеры использования:

```java
public class Main {  
    public static void main(String[] args) {  
        List<User> users = new ArrayList<>();  
        users.add(new User("Alex", 20));  
        users.add(new User("Jane", 30));  
        users.add(new User("Jack", 40));  
        users.add(new User("Jill", 50));  
        users.add(new User("Joe", 60));  
        users.add(new User("Jenny", 70));  
  
        int[] arr = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};  
        
        Stream.of(arr).forEach(System.out::println);  // первый способ
        
        Arrays.stream(arr).forEach(System.out::println);  // второй способ
          
        users.stream()  // третий способ
			.filter(user -> user.getName().contains("l"))  
			.findFirst()  
			.ifPresentOrElse((user -> System.out.println(user.getName().contains("l"))), () -> {  
				System.out.println("User not found...");  
			});  
    }  
}
```

