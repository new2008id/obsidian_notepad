#appMovies  #Layout #ViewGroup #CardView
### Основные понятия

###### Новый ViewGroup — CardView

`CardView` (он же карточка) — это `ViewGroup`, который хранит только один элемент (как и `ScrollView`), но его особенность заключается в том, что он помогает создавать дизайнерские `View-элементы` (округление, тени, наложение `View-элементов` для создания единого элемента и пр.). Обычно в него вставляют `ViewGroup`, нежели `View-элемент`.

 Для того, чтобы его использовать, нужно создать отдельный `Layout` в том же папке (`Layout`) и указать (в зависимости от задачи) `CardView` как корневой.
### Применение:

### Примеры использования:

```xml
<androidx.cardview.widget.CardView xmlns:android="http://schemas.android.com/apk/res/android"  
    xmlns:app="http://schemas.android.com/apk/res-auto"  
    xmlns:tools="http://schemas.android.com/tools"  
    android:layout_width="match_parent"  
    android:layout_height="wrap_content"  
    app:cardCornerRadius="8dp"  
    app:cardUseCompatPadding="true">  
  
    <androidx.constraintlayout.widget.ConstraintLayout                               android:layout_width="match_parent"  
        android:layout_height="wrap_content">  
  
        <ImageView android:id="@+id/imageViewPoster"  
            android:layout_width="match_parent"  
            android:layout_height="wrap_content"  
            android:adjustViewBounds="true"  
            android:contentDescription="@null"  
            app:layout_constraintTop_toTopOf="parent"  
            tools:src="@tools:sample/avatars" />  
  
        <TextView android:id="@+id/textViewRating"  
            android:layout_width="wrap_content"  
            android:layout_height="wrap_content"  
            android:layout_margin="16dp"  
            android:background="@android:color/holo_green_light"  
            android:padding="16dp"  
            android:textColor="@color/white"  
            android:textSize="16sp"  
            app:layout_constraintEnd_toEndOf="parent"  
            app:layout_constraintTop_toTopOf="parent"  
            tools:text="8.0"  
            />  
    </androidx.constraintlayout.widget.ConstraintLayout>  
</androidx.cardview.widget.CardView>
```

[[Movies Adapter]]
