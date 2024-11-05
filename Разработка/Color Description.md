#java #android #mobile 
## Внешний вид приложения
![[Pasted image 20241105140114.png]]
При выборе из select цвета, и нажатии на кнопку "Выберите цвет". Происходит вывод описания цвета.

## Разработка приложения

### Происходит создание layout для MainActivity.java

```xml 
<Spinner  
    android:id="@+id/spinner_color"  
    android:layout_width="409dp"  
    android:layout_height="wrap_content"  
    android:layout_marginTop="16dp"  
    android:entries="@array/colors"  
    app:layout_constraintEnd_toEndOf="parent"  
    app:layout_constraintHorizontal_bias="0.0"  
    app:layout_constraintStart_toStartOf="parent"  
    app:layout_constraintTop_toTopOf="parent" />  
  
<Button  
    android:id="@+id/button"  
    android:layout_width="0dp"  
    android:layout_height="wrap_content"  
    android:layout_marginTop="16dp"  
    android:text="@string/button_color_text"  
    android:onClick="showDescButton"  
    app:layout_constraintEnd_toEndOf="parent"  
    app:layout_constraintHorizontal_bias="1.0"  
    app:layout_constraintStart_toStartOf="parent"  
    app:layout_constraintTop_toBottomOf="@+id/spinner_color" />  
  
<TextView  
    android:id="@+id/description"  
    android:layout_width="350dp"  
    android:layout_height="84dp"  
    android:layout_marginTop="12dp"  
    android:visibility="invisible"  
    android:text="TextView"  
    app:layout_constraintEnd_toEndOf="parent"  
    app:layout_constraintStart_toStartOf="parent"  
    app:layout_constraintTop_toBottomOf="@+id/button" />
```

### Инициализация переменных для работы с layout
```java
private Spinner spinner;  
private TextView description;
```
Метод обязует реализовать метод *onCreate*(). Находим по ID - spinner и textView (description) 
```java
@Override  
protected void onCreate(Bundle savedInstanceState) {  
    super.onCreate(savedInstanceState);  
    EdgeToEdge.enable(this);  
    setContentView(R.layout.activity_main);  
    ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {  
        Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());  
        v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);  
        return insets;  
    });  
  
    spinner = findViewById(R.id.spinner_color);  
    description = findViewById(R.id.description);  
}
```

### Обработка обработчика события onClick для кнопки. 
```java
public void showDescButton(View view) {  
    int position = spinner.getSelectedItemPosition();  
    String descriptionText = getResources().getStringArray(R.array.colors_description)[position];  
    description.setText(descriptionText);  
    description.setVisibility(View.VISIBLE);  
}
```
Работает по принципу:
1. Находим выбранную позицию
2. Получаем из Resources строку по выбранной позиции
3. Устанавливаем текст для TextView (descritionText)
4. Устанавливаем свойство setVisibility - VISIBLE.