#Spinner #android #TextView  #appCafe 
### Реализация в `MakeOrderActivity`:

```xml
<Spinner  
    android:id="@+id/spinnerTea"  
    android:layout_width="match_parent"  
    android:layout_height="wrap_content"  
    android:layout_margin="8dp"  
    android:entries="@array/types_of_tea"  
    android:visibility="invisible"  
    app:layout_constraintBottom_toTopOf="@+id/buttonMakeOrder"  
    app:layout_constraintTop_toBottomOf="@+id/tvDrinkType" />  
/>  
  
<Spinner  
    android:id="@+id/spinnerCoffee"  
    android:layout_width="match_parent"  
    android:layout_height="wrap_content"  
    android:layout_margin="8dp"  
    android:entries="@array/types_of_coffee"  
    tools:visibility="visible"  
    android:visibility="invisible"  
    app:layout_constraintBottom_toTopOf="@+id/buttonMakeOrder"  
    app:layout_constraintTop_toBottomOf="@+id/tvDrinkType" />  
/>
```

>[!error ] Однако, нельзя просто так добавить текст, как у `TextView` и пр. Он требует иное добавление текста в string.xml — массива строк. ***Синтаксис массива***:

```xml
<string-array name="types_of_tea">  
    <item>Зеленый</item>  
    <item>Черный</item>  
</string-array>  
  
<string-array name="types_of_coffee">  
    <item>Американо</item>  
    <item>Эспрессо</item>  
    <item>Латте</item>  
</string-array>
```

`Array name` — имя массива; `item` — имя элемента.
После добавления нужно указать его уже в `Spinner`. Указываем через не `text`, а через `entries`.