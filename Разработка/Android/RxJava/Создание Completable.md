#Completable #Disposable #CompositeDisposable
### Основные понятия

Для этого нужно создать возвращаемый метод с типом данных `Completable` и вызвать статический метод `fromAction()`. Отличие от `fromCallable()` заключается в том, что не требует никакие данные (что свойственно `Completable`), в отличие от `fromCallable()`.
### Примеры использования:

*MainViewModel.java*
```java
public void removeNote(Note note) {  
    Disposable disposable = removeRx(note)  
            .subscribeOn(Schedulers.io())  
            .observeOn(AndroidSchedulers.mainThread())  
            .subscribe(new Action() {  
                @Override  
                public void run() throws Throwable {  
                    Log.d("MainViewModel", "Note: " + note.getId());  
                    refreshList();  
                }  
            });  
    compositeDisposable.add(disposable);  
}  
  
private Completable removeRx(Note note) {  
    return Completable.fromAction(new Action() {  
        @Override  
        public void run() throws Throwable {  
            noteDatabase.notesDao().remove(note.getId());  
        }  
    });  
}
```

### Как он теперь работает:

1. `removeRX()` также будет находится в ожидании, когда на remove не подпишутся
2. После подписки будет создан фоновый поток и будет вызван `run()` c `removeRX()`
3. После работы фонового потока, мы переключим на главный поток и будет вызвана логика в `subscribe()`

Такие же цели, как у [[Single]].
