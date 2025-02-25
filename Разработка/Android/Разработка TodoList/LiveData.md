#LiveData #DAO #onCreate #this #observe #Activity #Handler #Thread 
### Основные понятия

`LiveData` — это класс, на котором можно подписывать объекты, благодаря ему мы сможем автоматически реагировать на изменение у объекта. Или иное определение — это класс, который содержит данные и за поведением которого можно наблюдать 

>[!success ] Чтобы реализовать его, в нашем случае, нужно поменять логику в интерфейсе `NotesDao`:
### Применение:

```java
@Dao  
public interface NotesDao {  
    @Query("SELECT * FROM notes")  
    LiveData<List<Note>> getNotes();  // LiveData
    @Insert  
    void addNote(Note note);  
    @Query("DELETE FROM notes WHERE id = :id")  
    void removeNote(int id);  
}
```


Теперь мы можем его реализовать и подписаться в `onCreate()`. Для этого вызываем его через `getNotes()`. Теперь нужно вызвать метод, который подписывает объекты — `observe()` (наблюдение). У него два параметра:
- `LifecycleOwner owner` — требует жизненный цикл, достаточно дать ему `this` (`Activity`)
- `Observer<? super T> observer` — это функциональный интерфейс, который реализует `onChanged()`    

>[! ] Таким образом он подписывает `объект` (а конкретно таблицу) и проверяет, есть ли `данные`, если есть, то он отправляет их в `метод` из функционального `интерфейса`, дабы мы смогли с ними взаимодействовать. Также он снова отправит новые `данные` и вызовется, если произошли какие-либо изменения в подписанном `объекте`. 

>[!success ] Благодаря ему нам ненужно создавать `потоки` и `Handler`, всё делается под капотом.
### Примеры использования:

Теперь можно в `MainActivity` полностью избавиться от `handler` и от реализации метода `onResume()`, так теперь будет использовать `LiveData` и подписываться на изменение `объекта`

```java
noteDatabase.notesDao().getNotes().observe(this, new Observer<List<Note>>() {  
    @Override  
    public void onChanged(List<Note> notes) {  
        notesAdapter.setNotes(notes);  
    }  
});
```
