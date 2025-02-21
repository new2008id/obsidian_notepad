#RecyrclerView #View #Swipe #itemTouchHelper #SimpleCallback #Adapter #getter #ArrayList 
### Основные понятия

Для того, чтобы реализовать `swipe`, нужно реализовать в каком-то `Activity`. Нужно вызывать класс `ItemTouchHelper`. Это служебный класс нужен для поддержки `swipe` и перемещение `View-элементов` в `RecyclerView Adapter`; в параметре конструктора мы вызываем анонимный вложенный класс `SimpleCallback()`. 

Он переопределяет два метода: `onMove()` (перемещение `View-элементы`) и `onSwiped()` (`swipe`). Первый метод нам не нужен, а вот второй нужен. 

В `onSwiped()` мы можем спокойно скопировать логику из нашего слушателя, однако, вы получите ошибку, так как ссылка на `Note` не видна для него

```java
@Override  
public void onSwiped(@NonNull RecyclerView.ViewHolder viewHolder, int direction) {  
    database.removeNote(note.getId());  // Cannot resolve symbol 'note'
    showNotes();  
}
```
### Решение данной проблемы:

1. Создать переменную, которая будет получать позицию `view-элемента`, с которым происходит взаимодействия
2. Создать `геттер` для `ArrayList note`
3. Создать экземпляр класса `Note` через `ArrayList`, т. е. получить экземпляр `Note` через `get` и присвоить к ссылочной переменной `Note`.

```java
@Override  
public void onSwiped(@NonNull RecyclerView.ViewHolder viewHolder, int direction) {  
    int position = viewHolder.getAdapterPosition();  
    Note note = notesAdapter.getNotes().get(position);  
    database.removeNote(note.getId());  
    showNotes();  
}
```

Конструктор `SimpleCallback()` не пустой. Он хранит два параметра: `dragdirs` и `swipedirs`. Первый задает параметр для перемещения, второй направление (только вправо (`RIGHT`), только лево (`LEFT`) или оба (`LEFT | RIGHT`)) для `swipe` из `ItemTouchHelper`. Если вам не нужен из какой-либо параметра — ставьте `0`.

```java
ItemTouchHelper itemTouchHelper = new ItemTouchHelper(
new ItemTouchHelper.SimpleCallback(0, ItemTouchHelper.RIGHT | ItemTouchHelper.LEFT) {  
    @Override  
    public boolean onMove(@NonNull RecyclerView recyclerView,  
                          @NonNull RecyclerView.ViewHolder viewHolder,  
                          @NonNull RecyclerView.ViewHolder target) {  
        return false;  
    }  
  
    @Override  
    public void onSwiped(@NonNull RecyclerView.ViewHolder viewHolder, int direction) {  
        int position = viewHolder.getAdapterPosition();  
        Note note = notesAdapter.getNotes().get(position);  
        database.removeNote(note.getId());  
        showNotes();  
    }  
});
```

>[!warning ] После этих действий мы должны прикрепить его к `RecyclerView`

```java
itemTouchHelper.attachToRecyclerView(rvNotes);
```

[[Проблемы класса Database]]




