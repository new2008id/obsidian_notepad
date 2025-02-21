#Adapter #RecyrclerView #setter #notifyDataSetChanged #LayoutManager
### Основные понятия

После создания адаптера, нужно присоединить его к `RecyclerView`. Для этого нужно создать экземпляр класса самого `Adapter` и через метод `RecyclerView.setAdapter()` прикрепить его.

```java
    notesAdapter = new NotesAdapter();  
    rvNotes.setAdapter(notesAdapter);
```
### Применение:

Однако, нужно задать расположение элементов. Есть два способа: из кода и из макета. В нашем случае мы в макете добавляем `app:layoutManager=«»` и выбираем нужный параметр. В нашем случае нужно, чтобы элементы располагались вертикально

После этих манипуляций мы можем в самом адаптере указать список, который адаптер и будет выводить на экран.

```xml
<androidx.recyclerview.widget.RecyclerView  
    android:id="@+id/rvNotes"  
    android:layout_width="match_parent"  
    android:layout_height="match_parent"  
    app:layoutManager="androidx.recyclerview.widget.LinearLayoutManager"  
    tools:listitem="@layout/note_item"  
    tools:itemCount="5"/>
```

Также возможен быть такой баг: после добавления элементов список не изменится. Для этого нужно добавить в сеттере метод `notifyDataSetChanged()`, который и сообщит, что нужно обновить список в адаптере.

```java
public void setNotes(ArrayList<Note> notes) {  
    this.notes = notes;  
    notifyDataSetChanged(); // для обновления данных, не рекомендуемый способ  
}
```

Далее потребуется [[Добавление слушателей в адаптер]]


