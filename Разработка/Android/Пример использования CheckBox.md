#Checkbox #android 
### Примеры из проекта для реализации `MakeOrderActivity`:

```xml
<CheckBox  
    android:id="@+id/checkBoxSugar"  
    android:layout_width="wrap_content"  
    android:layout_height="wrap_content"  
    android:text="@string/sugar"  
    android:textColor="@color/purple_500"  
    app:layout_constraintBottom_toBottomOf="@+id/checkBoxMilk"  
    app:layout_constraintEnd_toStartOf="@+id/checkBoxMilk"  
    app:layout_constraintStart_toStartOf="parent"  
    app:layout_constraintTop_toTopOf="@+id/checkBoxMilk" />  
  
<CheckBox  
    android:id="@+id/checkBoxMilk"  
    android:layout_width="wrap_content"  
    android:layout_height="wrap_content"  
    android:text="@string/milk"  
    android:textColor="@color/purple_500"  
    app:layout_constraintBottom_toTopOf="@+id/tvDrinkType"  
    app:layout_constraintEnd_toStartOf="@id/checkBoxLemon"  
    app:layout_constraintHorizontal_bias="0.5"  
    app:layout_constraintStart_toEndOf="@id/checkBoxSugar"  
    app:layout_constraintTop_toBottomOf="@+id/tvAdditives" />  
  
<CheckBox  
    android:id="@+id/checkBoxLemon"  
    android:layout_width="wrap_content"  
    android:layout_height="wrap_content"  
    android:text="@string/lemon"  
    android:textColor="@color/purple_500"  
    app:layout_constraintBottom_toBottomOf="@id/checkBoxMilk"  
    app:layout_constraintEnd_toEndOf="parent"  
    app:layout_constraintStart_toEndOf="@id/checkBoxMilk"  
    app:layout_constraintTop_toTopOf="@+id/checkBoxMilk" />
```




