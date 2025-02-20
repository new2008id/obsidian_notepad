#View #Layout #TextView #LinearLayout #inflate 
### Основные понятия

>[! ] Может появится случай, когда нужно добавить `View-элемент` через код. Чтобы добавить `View-элемент`, нужно создать отдельный `Layout` и задать те параметры, которые будут соответствовать нашим требованиям.

>[!warning ] После создания мы можем спокойно сделать нужный `View-элемента` (если он единственный) родительным. Однако, например, если мы добавили `TextView` как родительный, это не означает, что он становится `View-группой`
### Примеры использования:

```xml
<TextView xmlns:android="http://schemas.android.com/apk/res/android"  
    xmlns:tools="http://schemas.android.com/tools"  
    android:id="@+id/tvNote"  
    tools:text="Hello"  
    tools:background="@android:color/holo_green_light"  
    android:textColor="@color/white"  
    android:padding="16dp"  
    android:layout_margin="8dp"  
    android:textSize="16sp"  
    android:layout_width="match_parent"  
    android:layout_height="wrap_content">  
</TextView>
```

Однако мы не можем просто добавить в `LinearLayout`, так как он может принимать только `View-элемент`. В данном моменте у нас макет, а не `View-элемент`. Чтобы преобразовать из макета в View-элемент нужно проделать следующие действия:

Нужно использовать класс `LayoutInFlater` и его метод `inflate()`, который преобразует макет в `View-элемент`. Синтаксис его такой: `id` — `View-элемент`, `ViewGroup` — `View-группа`, в которой будет вставлять элемент, `attachToRoot` — прикрепляет к родителю, обычно, ставится `false`, так как мы будем вручную прикреплять.

```java
private void showNotes() {  
    for (Note note : notes) {  
        View view = getLayoutInflater().inflate(  
                R.layout.note_item,  
                linearLayoutNotes,  
                false  
        );  
        TextView textViewNote = view.findViewById(R.id.tvNote);  
        textViewNote.setText(note.getText());  
  
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
        int color = ContextCompat.getColor(this, colorResId);  
        textViewNote.setBackgroundColor(color);  
        linearLayoutNotes.addView(view);  
    }  
}
```
### Краткие шаги:

>[!success ] Создать макет и реализовать `View-элемент`

>[!success ] Преобразовать макет в `View-элемент`

>[!success ] Добавить дополнительные параметры в `View-элементы`

>[!success ] Добавить сам в `View-группу`

[[Получение конкретного View-класса через родителя View]]