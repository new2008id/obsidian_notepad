#Runnable #Handler #Looper  #onResume #LiveData
### Основные понятия

Класс `Handler` является «мостом» между `основным и дочерним` потоками (в нашем случаем он будет держать ссылку на главном потоке). Он позволяет нам либо из главного, либо из дочернего потока отправлять сообщение, Чтобы указать ссылку на главный поток, нужно использовать метод `getMainLooper()` в параметре конструктора его. Теперь мы можем главному потоку отправлять сообщение из дочерних потоков. `Handler.post()` принимает `Runnable` и нужно у него вызвать метод `run()` и реализовать логику; фактически в дочернем потоке будет выполняться логика в главном потоке. Сообщения отправляются в `Handler`, чтобы он передал эти сообщения в главному в типа данных `Runnable`:

1. Запускается главный поток
2. Создается и запускается дочерний поток
3. В дочернем потоке запускается Handler
4. Handler отправляет сообщение к конструктору, который реализован в главном потоке.
5. Передает уже к главному потоку
6. Главный поток получает сообщение и обрабатывает у себя
### Примеры использования:

```java
private Handler handler = new Handler(Looper.getMainLooper());

Thread thread = new Thread(new Runnable() {  
    @Override  
    public void run() {  
        List<Note> notes = noteDatabase.notesDao().getNotes();  
        handler.post(new Runnable() {  
            @Override  
            public void run() {  
                notesAdapter.setNotes(notes);  
            }  
        });  
    }  
});  
thread.start();
```

```java
Thread thread = new Thread(new Runnable() {  
    @Override  
    public void run() {  
        noteDatabase.notesDao().addNote(note);  
        handler.post(new Runnable() { // вызываем на главном потоке  
            @Override  
            public void run() {  
                finish(); // завершаем работу Activity  
            }  
        });  
    }  
});  
thread.start();
```

Сейчас есть проблемы с методом `showNotes()` в `onResume()`.
```java
@Override  
protected void onResume() {  
    super.onResume();  
    showNotes();  
}
```

>[!warning ] Мы вызываем `showNotes()` в `onResume()` каждый раз, когда экран теряет фокус. Фокус может потеряться даже тогда, человек просто свернул приложение. Если в `onResume()` вызывается таким образом какая-то тяжелая логика, которая нагружает сильно телефон, то это лишняя трата ресурса системы телефона. Нам нужно реализовать так, чтобы `showNotes()` вызвался только тогда, когда действительно случилось изменение. Для этого существует специальный класс — [[LiveData]].

