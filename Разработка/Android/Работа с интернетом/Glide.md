#Glide #ProgressBar #ImageView #View #json #Gradle 
### Основные понятия

`ProgressBar` — это `view-элемент`, который отображает прогресс виде кружочка.
![[Pasted image 20250228102241.png]]
```xml
<ProgressBar  
    android:id="@+id/progressBar"  
    style="?android:attr/progressBarStyle"  
    android:layout_width="wrap_content"  
    android:layout_height="wrap_content"  
    app:layout_constraintBottom_toBottomOf="parent"  
    app:layout_constraintEnd_toEndOf="parent"  
    android:visibility="gone"  
    tools:visibility="visible"  
    app:layout_constraintStart_toStartOf="parent"  
    app:layout_constraintTop_toTopOf="parent" />
```

Теперь осталась последняя задача: установить изображение в `ImageView` из `JSON-запрос`. Сделать самостоятельно требуют множество махинаций, который только усложнит код и предоставит вагон багов. Чтобы выполнить эту задачу без этих проблем, — используется библиотека `Glide`. 

Фишка этой библиотеки заключается в том, что он может подгружать изображение, GIF-анимации и пр. файлы в асинхронном потоке и загружать всё в `View-элементе`. Нам ненужно заботиться о тяжелых махинаций, всё за нас делает `Glide`. 

>[!warning ] Нужно загрузить в качестве зависимости в `Gradle Module`.

После загрузки мы можем уже с ним работать.
### Примеры использования:

*MainActivity.java*
```java
viewModel.getDogImage().observe(this, new Observer<DogImage>() {  
    @Override  
    public void onChanged(DogImage dogImage) {  
        Glide  
                .with(MainActivity.this)  
                .load(dogImage.getMessage())  
                .into(imageView);  
    }  
});
```

>[!success] Далее требуется доработать приложение и создать обработчик события по кнопке. [[Оператор doOn]]


