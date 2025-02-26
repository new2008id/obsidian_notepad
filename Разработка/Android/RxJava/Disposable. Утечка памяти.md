#Disposable #Activity #ViewModel #onCleared #onDestroy #CompositeDisposable
### Основные понятия

>[!error ] Если воспользоваться методом `delay(int, TimeUnit)` в своем потоке и моментом закрыть `Activity`, то данный поток всё равно будет работать, даже когда `Activity` уничтожен. По этой причине мы ещё не решили проблему с утечкой памяти.
### Применение:

Метод `subscribe` имеет тип данных `Disposable`. Он дает нам возможность управлять цикл жизни потока и отменять подписки. Вы скорее всего заметили, что `subscribe` предупреждает нас о том, что мы не управляем поток. Благодаря `Disposable` дает нам эту возможность. 

ViewModel имеет цикл жизни, как и `Activity`. Чтобы уничтожить `Activity`, вызывается метод `onDestroyed()`; чтобы уничтожить `ViewModel`, вызывается метод `onCleared()`.

Для того, чтобы отменить подписку, вызывается метод `disposable.dispose()`. Его стоит вызывать, когда мы уничтожаем `Activity`, чтобы предотвратить утечку памяти. 

Если у нас много потоков, то явно не стоит создавать каждый раз ссылку на `disposable` для каждого потока. Для этого существует класс-коллекция — `CompositeDisposable`. Чтобы добавить `disposable` в коллекцию, используется метод `add()`. Для того, чтобы завершить все потоки в коллекции, достаточно вызвать тот же метод `dispose()`.
### Примеры использования:

*AddNoteViewModel.java*
```java
private Disposable disposable; // для одной подписки  
private CompositeDisposable compositeDisposable = new CompositeDisposable(); // для нескольких подписок

public void saveNote(Note note) {  
    Disposable disposable = notesDao.add(note)  
            .delay(5, TimeUnit.SECONDS)  
            .subscribeOn(Schedulers.io()) // происходит чтение и запись базы данных, в фоновом потоке  
            .observeOn(AndroidSchedulers.mainThread()) // переключает на главный поток  
            .subscribe(new Action() {  
                @Override  
                public void run() throws Throwable {  
                    Log.d("AddNoteViewModel", "subscribe");  
                    shouldCloseScreen.setValue(true);  
                }  
            });  
    compositeDisposable.add(disposable);  
}

@Override  
protected void onCleared() {  
    super.onCleared();  
    compositeDisposable.dispose();  
}
```


