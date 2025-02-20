#FloatingActionButton #View #Layout #LayoutInflater #inflate #LinearLayout #ContextCompat
### Основные понятия

`FloatingActionButton` (FAB) - это виджет в Android, представляющий собой круглую кнопку, обычно расположенную в углу экрана и “плавающую” над остальным контентом. 

>[! ] *Представляет собой следующую **кнопку***: 

![[Pasted image 20250220102919.png]]
### Применение:

Он используется для выполнения основного или наиболее важного действия на экране.
### Примеры использования:

```xml
<com.google.android.material.floatingactionbutton.FloatingActionButton  
    android:id="@+id/buttonAddNote"  
    android:layout_width="wrap_content"  
    android:layout_height="wrap_content"  
    android:layout_marginEnd="8dp"  
    android:layout_marginBottom="8dp"  
    android:contentDescription="@string/button_add"  
    app:layout_constraintBottom_toBottomOf="parent"  
    app:layout_constraintEnd_toEndOf="parent"  
    app:srcCompat="@android:drawable/ic_input_add" />
```

[[Добавление View-элемента в макет через код]]
