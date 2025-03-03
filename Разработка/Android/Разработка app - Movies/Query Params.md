#json #Query 
### Основные понятия

##### Динамическое изменение end-point

>[!warning ] Когда нам нужно изменять результат из `JSON-ответа` (например в `search`), то есть возможность менять `end-point` с кода: использовать аннотацию `@Query(«name»)`.

>[!warning ] В `Query` пишем нужный параметр для него. В результате чего мы будем получать каждый раз новый ответ. Если параметр до сих пор используется в `end-point`, то нужно удалить его.
### Примеры использования:

```java
public interface ApiService {  
    @GET("movie?rating.kp=7-10&sortField=votes.kp&sortType=-1&limit=5&year=2025&type=movie&token=MXTGTC1-GWVMXHR-NYNPSHM-XRJ4XCN")  
    Single<MovieResponse> loadMovies(  
            @Query("page") int page  
    );  
}
```

*Изменения в MainViewModel.java*
```java
public class MainViewModel extends AndroidViewModel {  
    private final MutableLiveData<List<Movie>> movies = new MutableLiveData<>();  
    private static final String TAG = "MainViewModel";  
    private int page = 1;  
    private final CompositeDisposable compositeDisposable = new CompositeDisposable();  
    public MainViewModel(@NonNull Application application) {  
        super(application);  
    }  
  
    public LiveData<List<Movie>> getMovies() {  
        return movies;  
    }  
  
    public void loadMovies() {  
        Disposable disposable = ApiFactory.apiService.loadMovies(page)  
                .subscribeOn(Schedulers.io())  
                .observeOn(AndroidSchedulers.mainThread())  
                .subscribe(new Consumer<MovieResponse>() {  
                    @Override  
                    public void accept(MovieResponse movieResponse) throws Throwable {  
                        page++;  
                        movies.setValue(movieResponse.getMovies());  
                    }  
                }, new Consumer<Throwable>() {  
                    @Override  
                    public void accept(Throwable throwable) throws Throwable {  
                        Log.d(TAG, throwable.toString());  
                    }  
                });  
  
        compositeDisposable.add(disposable);  
    }  
  
    @Override  
    protected void onCleared() {  
        super.onCleared();  
        compositeDisposable.dispose();  
    }  
}
```
