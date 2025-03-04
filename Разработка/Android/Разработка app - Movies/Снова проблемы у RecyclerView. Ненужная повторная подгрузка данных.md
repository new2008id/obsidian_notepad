#RecyrclerView #MVVM #ViewModel #null #MutableLiveData #appMovies 
### Основные понятия

Проблема заключается в следующем: когда мы доходим до того количества элементов у списка, у нас начинается вызываться метод подгрузки данных; однако, слушатель вызывается 10 раз и по этой причине будет 10 раз загружены страницы, а это в общем 300 кино сразу! Причина заключается в том, что эти 10 раз нужны для плавной прокрутки, но то время 10 раз, повторяюсь, вызывается слушатель. Чтобы решить данную проблему, нужно провернуть следующие действия:
- Создаем MLD, который хранит Boolean
- Проверка заключается в следующем: если MLD не является null и он хранит true — выйти из метода.     
- Если false, то вызвать основную логику подгрузку данных
### Примеры использования:

*MainViewModel.java*
```java
private final MutableLiveData<Boolean> isLoading = new MutableLiveData<>(false);

public LiveData<Boolean> getIsLoading() {  
    return isLoading;  
}

public void loadMovies() {  
    Boolean loading = isLoading.getValue();  
    if (loading != null && loading) {  
        return;  
    }
    ...
}
```

Благодаря этому метод будет вызван всего лишь один раз, так как эта операция не быстрая, в отличие от `RecyclerView`.

Следующая проблема, которая решается 3-мя кликами. Если у вас вызывается излишний раз метод из-за переворота экрана, но при этом вы используете `MVVM`, то можно этот метод положить в конструкторе `ViewModel`.

*MainViewModel.java*
```java
public MainViewModel(@NonNull Application application) {  
    super(application);  
    loadMovies();  
}
```