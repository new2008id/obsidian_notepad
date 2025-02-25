#ViewModel #ViewModelProvider #Activity 
### Основные понятия:

Дабы решить эту проблему, нужно переделать создание экземпляра класса `ViewModel` следующим образом:
```java
viewModel = new ViewModelProvider(this).get(MainViewModel.class);
```

Благодаря таким образом `ViewModel` будет жить, даже когда `Activity` будет пересоздан.

В конструкторе требуется владельца `ViewModel`, в нашем случае это `Activity`. `Get` — класс `ViewModel`.

Всегда используйте такой способ создания `ViewModel` в `View`.

ViewModel будет жить до тех пор, пока не будет вызван метод `finish()`.






