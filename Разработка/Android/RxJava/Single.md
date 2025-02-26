#Single #Completable #CompositeDisposable #LiveData #MutableLiveData #setter #RxJava 
### Основные понятия

###### Отличие от Completable

Оба класса фактически одинаковы, они оба возвращают сведение о том, что метод завершил работу. Однако, `Completable` ничего не возвращает из типа данных, то бишь если мы ожидаем получить ещё взамен какие-либо данные (допустим, получаем данные из интернета), то мы ничего не получим.

>[! ] Особенно виднеется разница в `subscribe`:

 >[!warning ] В `Completable` переопределяется метод `run()` от `Action` без параметров, таким образом мы можем только указать логику о том, что метод завершился.
    
>[!warning ] В `Single` переопределяется метод  `accept(List<Note> notes)` от `Consumer` с параметром, таким образом мы можем не только указать логику о том, что метод завершил работу, но и также работать с данными из параметров в `accept()`.

Для этого существует класс `Single` — он имеет возможность не только вернуть сведение о завершении, но и также данные. 
###### Использование `Single` как замена `LiveData` в `NoteDao`

Для этого нужно заменить тип данных в `NoteDao` с `LiveData` на `Single`.

Скорее всего `getNotes()` будет жаловаться, что передается не LD, а `Single`. Для этого мы будем использовать `setter` — `MutableLiveData`, в котором мы будем класть данные из `Single`.
### Применение:

*NotesDao.java*
```java
@Dao  
public interface NotesDao {  
    @Query("SELECT * FROM notes")  
    Single<List<Note>> getNotes();  // помечаем тип Signle RxJava
  
    @Insert  
    Completable add (Note note);  
  
    @Query("DELETE FROM notes WHERE id = :id")  
    Completable remove(int id);  
}
```
### Примеры использования:

*MainViewModel.java*
```java
private final CompositeDisposable compositeDisposable = new CompositeDisposable();  
private MutableLiveData<List<Note>> notes = new MutableLiveData<>();

public LiveData<List<Note>> getNotes() {  
    return notes;  
}

public void refreshList() {  
    Disposable disposable = noteDatabase.notesDao().getNotes()  
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
```

*MainActivity.java*
```java
@Override  
protected void onResume() {  
    super.onResume();  
    viewModel.refreshList();  
}
```


