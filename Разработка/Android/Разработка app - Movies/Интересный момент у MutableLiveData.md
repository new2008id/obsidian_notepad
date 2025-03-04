#java #MutableLiveData #null #appMovies 

>[! ] Код на языке `Java`

>[!success ] Если нужно, чтобы у `MutableLiveData` был добавлен ещё список (элементы), то нужно провернуть вот такие действия:

*MainViewModel.java*
```java
public void loadMovies() {  
    Disposable disposable = ApiFactory.apiService.loadMovies(page)  
            .subscribeOn(Schedulers.io())  
            .observeOn(AndroidSchedulers.mainThread())  
            .subscribe(new Consumer<MovieResponse>() {  
                @Override  
                public void accept(MovieResponse movieResponse) throws Throwable {  
                    List<Movie> loadedMovies = movies.getValue();  
                    if (loadedMovies != null) {  
                        loadedMovies.addAll(movieResponse.getMovies());  
                        movies.setValue(loadedMovies);  
                    } else {  
                        movies.setValue(movieResponse.getMovies());  
                    }  
                    page++;  
                }  
            }, new Consumer<Throwable>() {  
                @Override  
                public void accept(Throwable throwable) throws Throwable {  
                    Log.d(TAG, throwable.toString());  
                }  
            });  
  
    compositeDisposable.add(disposable);  
}
```

Мы создаем список и заполняем его старой список, если есть конечно. После этого проверяем: не является список пустым (`null`):
- Если да, то мы `MutableLiveData` устанавливаем список, полученные из параметра с метода
- Если нет, то мы у нового списка добавляем новый список, который мы получили из параметра, и мы вставляем наш список в `MutableLiveData`

>[!error ] Таким образом `MutableLiveData` не будет удаляться предыдущий список, а наоборот: будет соединять со старым с новым.

[[Снова проблемы у RecyclerView. Ненужная повторная подгрузка данных]]