#RxJava #map #Function #appMovies 
### Основные понятия

Оператор `map` нужен для того, чтобы сократить длинные вызовы в один вызов. Короче говоря он преобразует один тип данных в другую, они могут быть разными. Для этого нужно использовать интерфейс `Function<old, new>` и его метод `apply`, в котором мы вернём `old` и после этого оператора будет использоваться только `new`.
### Примеры использования:

*MovieDetailViewModel.java*
```java
public void loadTrailers(int id) {  
    Disposable disposable = ApiFactory.apiService.loadTrailers(id)  
            .subscribeOn(Schedulers.io())  
            .observeOn(AndroidSchedulers.mainThread())  
            .map(new Function<TrailerResponse, List<Trailer>>() {  
                @Override  
                public List<Trailer> apply(TrailerResponse trailerResponse) throws Throwable {  
                    return trailerResponse.getTrailersList().getTrailers();  
                }  
            })  
            .subscribe(new Consumer<List<Trailer>>() {  
                @Override  
                public void accept(List<Trailer> trailersList) throws Throwable {  
                    trailers.setValue(trailersList);  
                }  
            }, new Consumer<Throwable>() {  
                @Override  
                public void accept(Throwable throwable) throws Throwable {  
                    Log.d(TAG, "throwable: " + throwable.toString());  
                }  
            });  
    compositeDisposable.add(disposable);  
}
```
