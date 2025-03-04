#appMovies #Serializable #string #Intent 
### Основные понятия

>[!warning ] Если нужно передать класс в, например, `Intent`, то он не сможет передать, так как `Intent` не будет поддерживать ваш класс. Чтобы решить проблему, мы можем передать класс по байтом благодаря интерфейсу `Serializable`. 

>[!warning ] Данный интерфейс является маркером, потому что он ничего не хранит. Все поля должны также сериализованными. 

>[!warning ] По умолчанию примитивные типы и `String` автоматически делаются, если есть ваши классы, то им тоже нужно добавить этот интерфейс.
### Примеры использования:

```java
public class Movie implements Serializable {
	...
	...
}

public class Poster implements Serializable {
	...
}

public class Rating implements Serializable {
	...
}
```

