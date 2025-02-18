#View #RadioGroup #RadioButton #Checkbox #Spinner
### Основные понятия

Изначально можно подумать, что можно множество раз использовать View-группу как вложенные друг у друга. Вы можете так использовать, однако, есть большой риск ухудшения производительности. Если макет сложный и решается возможно только через вложенные View-группы, то лучше использовать [[ConstraintLayout]], он позволяет создавать сложные макеты, в не ущерб производительности.

#### RadioGroup и RadioButtom

>[! ] `RadioGroup` является контейнером для `RadioButtom` (как и в принципе [[LinearLayout]] и пр.). По умолчанию ориентация у него вертикально. Чтобы задать ориентацию, используется `android:orientation`. 

>[!success ] `RadioButtom` это просто кнопки `off/on` для одной из них, выбор другого делает иное `off`

 >[!warning ] Для того, чтобы элемент занимал определенное место (например, в центре), используется `android:gravity`.
### Применение:

```xml
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"  
    xmlns:app="http://schemas.android.com/apk/res-auto"  
    xmlns:tools="http://schemas.android.com/tools"  
    android:id="@+id/main"  
    android:layout_width="match_parent"  
    android:layout_height="match_parent"  
    tools:context=".MakeOrderActivity">  
  
    <TextView android:id="@+id/tvGreetings"  
        android:layout_width="match_parent"  
        android:layout_height="wrap_content"  
        android:layout_margin="8dp"  
        android:text="@string/greetings"  
        android:textAlignment="center"  
        android:textColor="@color/purple_500"  
        android:textSize="24sp"  
        app:layout_constraintBottom_toTopOf="@+id/radioGroupDrinks"  
        app:layout_constraintTop_toTopOf="parent" />  
  
    <RadioGroup android:id="@+id/radioGroupDrinks"  
        android:layout_width="match_parent"  
        android:layout_height="wrap_content"  
        android:gravity="center"  
        android:orientation="horizontal"  
        app:layout_constraintBottom_toTopOf="@+id/tvAdditives"  
        app:layout_constraintTop_toBottomOf="@+id/tvGreetings">  
  
        <RadioButton android:id="@+id/radioButtonTea"  
            android:layout_width="wrap_content"  
            android:layout_height="wrap_content"  
            android:layout_margin="8dp"  
            android:text="@string/tea"  
            android:textColor="@color/purple_500" />  
  
        <RadioButton android:id="@+id/radioButtonCoffee"  
            android:layout_width="wrap_content"  
            android:layout_height="wrap_content"  
            android:layout_margin="8dp"  
            android:text="@string/coffee"  
            android:textColor="@color/purple_500" />  
    </RadioGroup>
```

#### CheckBox

`CheckBox` - это просто галочки, *выглядят они так:*

![[Pasted image 20250218115329.png]]
[[Пример использования CheckBox]]
#### Spinner и новое ключевое слово у string.xml

>[! ] `Spinner` — это выпадающий список, который человек может выбрать из него. Как он выглядит:

![[Pasted image 20250218115220.png]]

[[Пример использования Spinner]]

