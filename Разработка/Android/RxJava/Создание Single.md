#Single #Disposable #CompositeDisposable 
### Основные понятия

Для того, чтобы использовать тип данных `Single`, нужно создать возвращаемый метод, чтобы создать `Single`, используется статический метод `fromCallable()`.

Данный метод требует реализацию получения данных, в нашем случае. Метод из функционального интерфейса `call()` будет хранить такой тип данных, в котором мы указали в дженериках.
### Примеры использования:

*MainViewModel.java*
```java
public void refreshList() {  
    Disposable disposable = getNotesRx()  
            .subscribeOn(Schedulers.io())  
            .observeOn(AndroidSchedulers.mainThread())  
            .subscribe(new Consumer<List<Note>>() {  
                @Override  
                public void accept(List<Note> notesFromDb) throws Throwable {  
                    notes.setValue(notesFromDb);  
                }  
            });  
    compositeDisposable.add(disposable);  
}  
  
private Single<List<Note>> getNotesRx() {  
    return Single.fromCallable(new Callable<List<Note>>() {  
        @Override  
        public List<Note> call() throws Exception {  
            return noteDatabase.notesDao().getNotes();  
        }  
    });  
}
```

### Как он теперь работает:

1. `getNotesRX()` находится в ожидании, когда метод `refleshList()` будет подписан
2. После подписки получение данные из БД произойдет в фоновом потоке
3. После переключения на главный поток данные из БД прилетят спокойно в `subscribe()`

Таким образом мы можем спокойно создавать методы на основе `Single`. Также данный подход подходит, если у вас есть тяжелые операции и вы не хотите нагружать главный поток.