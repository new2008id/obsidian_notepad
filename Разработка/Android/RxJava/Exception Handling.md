#RxJava #Thread #onError #subscribeOn #Exception 
### Основные понятия

>[! ] Как у `Thread`, есть вероятность получить исключение во время работы потоков. В RxJava на первый взгляд не имеет обработчик исключений как будто и повышается риск `crash` из-за невозможности обработки исключений. 

>[! ] На самом деле в `subscribe()` есть второй параметр, а именно `onError`, в нём мы должны реализовать метод, который будет вызываться при получение `исключения`.
### Примеры использования:

*MainViewModel.java*
```java
public void removeNote(Note note) {  
    Disposable disposable = noteDatabase.notesDao().remove(note.getId())  
            .subscribeOn(Schedulers.io())  
            .observeOn(AndroidSchedulers.mainThread())  
            .subscribe(new Action() {  
                @Override  
                public void run() throws Throwable {  
                    Log.d("MainViewModel", "Note: " + note.getId());  
                }  
            }, new Consumer<Throwable>() {  
                @Override  
                public void accept(Throwable throwable) throws Throwable {  
                    Log.d("MainViewModel", "Error: " + throwable.getMessage());  
                }  
            });  
    compositeDisposable.add(disposable);  
}
```

*AddNoteViewModel.java*
```java
public void saveNote(Note note) {  
    Disposable disposable = notesDao.add(note)  
            .subscribeOn(Schedulers.io()) // происходит чтение и запись базы данных, в фоновом потоке  
            .observeOn(AndroidSchedulers.mainThread()) // переключает на главный поток  
            .subscribe(new Action() {  
                @Override  
                public void run() throws Throwable {  
                    Log.d("AddNoteViewModel", "subscribe");  
                    shouldCloseScreen.setValue(true);  
                }  
            }, new Consumer<Throwable>() {  
                @Override  
                public void accept(Throwable throwable) throws Throwable {  
                    Log.d("AddNoteViewModel", "error: " + throwable.getMessage());  
                }  
            });  
    compositeDisposable.add(disposable);  
}
```

>[!warning ] В `RxJava` стараться всегда делать проверку на ошибки