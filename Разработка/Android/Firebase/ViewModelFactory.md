#Firebase #Context #ViewModelProvider #ViewModelProviderFactory #ViewModel  
### Основные понятия

###### Когда в параметре конструкта не стандартное

Если конструктор у вас принимает ни `Context`, ни ничего, а свои нужные параметры, то обыкновенно через класс `ViewModelProvider`, то у вас ничего не получится сделать и приложение упадет с ошибками. А ошибка заключается в том, что данный класс не понимает ваши параметры. Для того, чтобы воспользоваться конструктором со своими параметрами, нужно создать собственный класс и расшириться от интерфейса `ViewModelProvider.Factory`.
###### Создаем класс

В первом очереди мы создаем нам нужный конструктор, который будет принимать нужные параметры.

После того этого мы переопределяем метод `create` и указываем в `return` `класс-VM`, где мы здесь указываем нужные параметры. Он создаст экземпляр `класса-VM` с нужными параметрами. 
###### Используем

Для того, чтобы использовать `Factory`, достаточно указать его в конструкторе `ViewModelProvider`. В принципе всё также.
### Примеры использования:

```java
public class ChatViewModelFactory implements ViewModelProvider.Factory {  
  
    private String currentUserId;  
    private String otherUserId;  
  
    public ChatViewModelFactory(String currentUserId, String otherUserId) {  
        this.currentUserId = currentUserId;  
        this.otherUserId = otherUserId;  
    }  
  
    @NonNull  
    @Override    public <T extends ViewModel> T create(@NonNull Class<T> modelClass) {  
        return (T) new ChatViewModel(currentUserId, otherUserId);  
    }  
}
```


