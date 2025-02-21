#ViewHolder #itemView #View #RecyrclerView #onCreateViewHolder #return #onBindViewHolder
### Основные понятия

>[! ] В типе данных метода `onCreateViewHolder()` указываем нашу реализацию. 

>[!warning ] И в `return` возвращаем экземпляр класса, который принимает `view-элемент`. 

>[!error ] Таким образом у нас `пересобираются` из макета в `view-элементы` и находим их всего лишь `10-12 раз`.
### Примеры использования:

```java
@NonNull  
@Override  
public NotesViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {  
    View view = LayoutInflater.from(parent.getContext()).inflate(  
            R.layout.note_item,  
            parent,  
            false  
    );  
    return new NotesViewHolder(view);  
}
```

### Реализация `onBindViewHolder()`

В параметре метода `onBindViewHolder()` указываем наш `ViewHolder` - `NotesViewHolder`. Чтобы изменить параметр для `View-элемента` (в нашем случае `TextView`), то из параметра используем `viewHolder`, который и хранит ссылку на `View-элемент`(`TextView`). А чтобы получить контекст, то мы делаем через переменную `itemView`.

```java
@Override  
public void onBindViewHolder(NotesViewHolder viewHolder, int position) {  
    Note note = notes.get(position);  
    viewHolder.textViewNote.setText(note.getText());  
  
    int colorResId;  
    switch (note.getPriority()) {  
        case 0:  
            colorResId = android.R.color.holo_green_light;  
            break;  
        case 1:  
            colorResId = android.R.color.holo_orange_light;  
            break;  
        default:  
            colorResId = android.R.color.holo_red_light;  
    }  
    int color = ContextCompat.getColor(viewHolder.itemView.getContext(), colorResId);  
    viewHolder.textViewNote.setBackgroundColor(color);  
}
```

>[!warning ] И обязательно нужно указывать в обобщении наш `ViewHolder`.

```java
public class NotesAdapter extends RecyclerView.Adapter<NotesAdapter.NotesViewHolder> {
	...
	...
}
```

Теперь необходимо [[Установка адаптера в RecyclerView]]