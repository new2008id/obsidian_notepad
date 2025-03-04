#drawable #TextView #ContextCompat #appMovies 
### Основные понятия

###### Создаем круглые backgrounds

Для того, чтобы сделать отзывы круглыми, нужно создать файл в папке `Drawable`. В «`Root Element`» указываем `shape`. 

У корневого элемента указываем, какая фигура должна отображаться, а для того, чтобы указать, используется параметр `android:shape`, указываем `oval`. 

Для того, чтобы дать цвету кругу, используется параметр <solid android:color=«»/>. Для того, чтобы использовать системные цвета, нужно сперва указать «`android`», а потом «`color`».

Для того, чтобы указать отступы, используется `<padding/>`.
### Примеры использования:

```xml
<shape xmlns:android="http://schemas.android.com/apk/res/android"  
    android:shape="oval">  
    <solid android:color="@android:color/holo_green_light" />  
    <padding        android:bottom="8dp"  
        android:left="8dp"  
        android:right="8dp"  
        android:top="8dp" />  
</shape>
```

### Установка Background из кода

>[!warning ] Установка происходит, как с установкой цвета. Мы получаем `id` у `background` нашего и создаем переменную типы `Drawable` и инициализируем через `ContextCompat`, чтобы он уже имел не `id`, а сам `background`. После этих манипуляций можно уже устанавливать его в `TextView`.

*MoviesAdapter.java*
```java
@Override  
public void onBindViewHolder(@NonNull MoviesViewHolder holder, int position) {  
    Movie movie = movies.get(position);  
    Glide  
            .with(holder.itemView)  
            .load(movie.getPoster().getUrl())  
            .into(holder.imageViewPoster);  
  
    double rating = movie.getRating().getKp();  
    int backgroundId;  
    if (rating > 7) {  
        backgroundId = R.drawable.circle_green;  
    } else if (rating > 5) {  
        backgroundId = R.drawable.circle_orange;  
    } else {  
        backgroundId = R.drawable.circle_red;  
    }  
    Drawable background = ContextCompat.getDrawable(holder.itemView.getContext(), backgroundId);  
    holder.textViewRating.setBackground(background);  
    holder.textViewRating.setText(String.valueOf(rating));  
}
```