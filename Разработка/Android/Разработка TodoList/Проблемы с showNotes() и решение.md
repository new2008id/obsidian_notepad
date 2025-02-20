#Singleton #Activity #finish #LinearLayout #onCreate #onPause #onStart #onResume #onRestart 
### Основные понятия

>[!success ] Если вам нужно завершить работу `Acitivity`, используется метод `finish()`

В конкретном нашем случае у нас не обновляется список из-за двух причин:

1. Метод `showNotes()` вызывается один раз, то бишь в методе `onCreate()`. 
2. При переключение из одной экрана в другую, предыдущий экран не уничтожается, он просто останавливается работу (`onPause()`, `onStop()`) и возобновляет свою работу при возращения (`onRestart()`, `onStart()`, `onResume()`). 
3. По этой причине `showNotes()` вызывается один раз. 
4. Данную проблему легко решить: перенести вызов метода `showNotes()` в какую-нибудь метод, такие как: `onRestart()`, `onStart()` или `onResume()`.

Связи тем, что `showNotes()` теперь вызывается каждый раз после возобновления экрана, он начнёт дублировать элементы. 
Чтобы такого не было, нужно заставить `LinearLayout` очищать каждый раз список перед вызов всей кода в этого метода, дабы предотвратить дублирование. 
Чтобы очистить элементы в `LinearLayout`, используется метод `removeAllViews()`

[[Простая реализация паттерна Singleton]]
### Примеры использования:

```java
@Override  
protected void onResume() {  
    super.onResume();  
    showNotes();  
}

private void showNotes() {  
    linearLayoutNotes.removeAllViews();  
    for (Note note : database.getNotes()) {  
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

```java
private void saveNote() {  
    String text = etEnterNote.getText().toString().trim();  
    if (text.isEmpty()) {  
        Toast.makeText(  
                this,  
                "Введите описание заметки",  
                Toast.LENGTH_SHORT  
        ).show();  
    } else {  
        int priority = getPriority();  
        int id = database.getNotes().size();  
        Note note = new Note(id, text, priority);  
        database.addNote(note);  
  
        finish(); // завершаем работу Activity  
        Log.d("AddNoteActivity", "Note saved: " + note.toString());  
    }  
}
```


