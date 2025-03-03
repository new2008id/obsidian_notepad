### Основные понятия

Если посмотреть на этот код, то можно увидеть нарушение структуры в RxJava:
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXezTX422b-icaWW159L8BrQ7VMM9F-TjT8Ws5wNgFWcso3o4bji7ey76irvStcGFdLsPwVVrSZ12SH2M51uU7ZPoOzuYGDBCafGAy84ZZrJnlA8r2EEfHwddjL-ASvIplI4oE0iYVy6j7GYxjmQxwk?key=XG-G72NMuDbNrBBB_stoyr_0)

Во-первых мы вызываем первый метод до вызова потока и во-вторых вызываются в subscribe дважды. Код работает, но он нарушает стиль RxJava. Чтобы правильно написать нужно сделать следующие действия
### Улучшение кода

Решим первую проблему, а именно у первого метода. Он должен вызваться до или в моменте подписки потока. Для этого есть метод — doOnSubscribe(). В нём мы указываем логику, она будет вызвана во время (до) подписки.

Решим уже вторую проблему, а именно повторение двух методов в удачном и ошибочном завершении. Эта логика должна вызываться после завершения всех логики в subscribe() (реагировать на окончании потока), неважно, корректно или с ошибкой завершились. Для этого есть метод — doAfterTerminate(). В нём мы указываем логику, она будет вызвана после завершении всей логики у потока.

Если нужно реагировать на ошибку после завершения всей логике, можно использовать метод doOnError().
### Примеры использования:

*MainViewModel.java*
```java
public void loadDogImage() {  
    Disposable disposable = loadDogImageRx()  
            .subscribeOn(Schedulers.io())  
            .observeOn(AndroidSchedulers.mainThread())  
            .doOnSubscribe(new Consumer<Disposable>() {  
                @Override  
                public void accept(Disposable disposable) throws Throwable {  
                    isLoading.setValue(true);  
                    isError.setValue(false);  
                }  
            })  
            .doAfterTerminate(new Action() {  
                @Override  
                public void run() throws Throwable {  
                    isLoading.setValue(false);  
                }  
            })  
            .doOnError(new Consumer<Throwable>() {  
                @Override  
                public void accept(Throwable throwable) throws Throwable {  
                    isError.setValue(true);  
                }  
            })  
            .subscribe(new Consumer<DogImage>() {  
                @Override  
                public void accept(DogImage image) throws Throwable {  
                    dogImage.setValue(image);  
                }  
            }, new Consumer<Throwable>() {  
                @Override  
                public void accept(Throwable throwable) throws Throwable {  
                    Log.e(TAG, throwable.getMessage());  
                }  
            });  
  
    compositeDisposable.add(disposable);  
}
```


