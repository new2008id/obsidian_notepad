#optional #parallelStream #null 
### Основные понятия

`Optional<T>` — это класс-контейнер, который может содержать или не содержать значение типа `T`. Он предназначен для решения проблемы `NullPointerException` (NPE) и улучшения читаемости кода, делая более явным, что значение может отсутствовать.

>[! ] **Избежание NPE:** Вместо возврата `null`, метод может вернуть `Optional<T>`, что явно указывает на возможность отсутствия значения. Клиентский код должен явно проверить наличие значения в `Optional` перед его использованием.
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
  
        Optional<User> oldest = users.stream()  
                .filter(user -> user.getName().contains("l"))  
                .findFirst();  
	
		users.stream()  
        .filter(user -> user.getName().contains("l"))  
        .findFirst()  
        .ifPresentOrElse((user -> 
	        System.out.println(user.getName().contains("l"))), () -> {  
            System.out.println("User not found...");  
        });
  
  
        oldest.ifPresentOrElse((user -> System.out.println(user.getName().contains("l"))), () -> {  
            System.out.println("User not found...");  
        });  
  
        oldest.ifPresentOrElse((user -> {  
            if (user.getName().contains("l")) {  
                System.out.println(user.getName());  
            }  
        }), () -> System.out.println("User not found..."));  
  
  
        Optional<User> oldest1 = users.stream()  
                .filter(user -> user.getAge() < 5)  
                .max((Comparator.comparing(User::getAge)));  
  
        oldest1.ifPresent((user -> System.out.println(user.getName())));  
        oldest1.ifPresentOrElse((user -> System.out.println(user.getName())), () -> System.out.println("User not found..."));  
  
        if (oldest1.isPresent()) {  
            System.out.println(oldest.get().getName());  
        }  
    }  
}
```

Некоторые методы, такие как поиск элемента, получение максимального или
минимального значения возвращают тип `Optional`.

Тип `Optional` — контейнер для результата, он может содержать или не содержать значение.
Чтобы получить значение из Optional, нужно вызвать метод `get()`, предварительно сделав
проверку через `isPresent()`, либо используя функциональный стиль - через метод `ifPresent()` или `ifPresentOrElse()`

[[Способы создания Stream]]

Здесь будет описан [[Метод parallelStream()]]
