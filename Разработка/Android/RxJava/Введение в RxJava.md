#RxJava #Gradle #Room #Completable #Callback #subscribeOn #observeOn
### Основные понятия

>[!warning ] Для того, чтобы использовать эту библиотеку, нужно добавить его в `Gradle Module`.

>[!warning ] Однако, `Room` требует ещё одну зависимость, если мы собираемся работать с `RxJava`.
### Применение:

Для того, чтобы подписать метод `add` из `NotesDAO`, нужно изменить `void` на `Completable`, он нужен для того, чтобы сообщить `Rxjava` о завершении работы метода (и также для `callback`). 

Если нужен `callback`, то используется метод `subscribe(new Action {})`. Код внутри `Action` будет работать после завершения работы метода (в нашем случае `add`). 

Если нам нужно, чтобы код выполнялся в фоновом потоке, используется `subscribeOn()` и в качестве параметра `Schedulers.io()`. Первый метод переключает логику на указанный поток, а второй указывает, в каком именно потоке, в нашем случае в `io()` — работа с данными

Для того, чтобы логика в `subscribe` работала в главном потоке, нужно указать метод `observeOn(AndroidSchedulers.mainThread())`
### Примеры использования:

*Реализация для `AddNoteViewModel`*
```java
public void saveNote(Note note) {  
    notesDao.add(note)  
            .subscribeOn(Schedulers.io()) // происходит чтение и запись базы данных, в фоновом потоке  
            .observeOn(AndroidSchedulers.mainThread()) // переключает на главный поток  
            .subscribe(new Action() {  
                @Override  
                public void run() throws Throwable {  
                    shouldCloseScreen.setValue(true);  
                }  
            });  
}
```

[[Дополнительные сведения о subscribeOn() и observeOn()]]
