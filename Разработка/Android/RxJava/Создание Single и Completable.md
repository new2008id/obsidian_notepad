#RxJava #Single #Completable 
### Когда нет поддержки RxJava

Бывает такие моменты, когда нужная библиотека не поддерживает работу с RxJava и из-за этого у нас не будут работать потоки. 

Чтобы решить данную проблему, нужно создать свои методы на основе Single или Completable.
### Применение:

*NotesDao.java*
```java
@Dao  
public interface NotesDao {  
//    @Query("SELECT * FROM notes")  
//    Single<List<Note>> getNotes();  
//  
//    @Insert  
//    Completable add (Note note);  
//  
//    @Query("DELETE FROM notes WHERE id = :id")  
//    Completable remove(int id);  
  
    @Query("SELECT * FROM notes")  
    List<Note> getNotes();  
  
    @Insert  
    void add (Note note);  
  
    @Query("DELETE FROM notes WHERE id = :id")  
    void remove(int id);  
}
```

На основе текущего interface - `NotesDao`, следует переделать реализации - [[Создание Single]] и [[Создание Completable]]



