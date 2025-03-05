#ScrollView #android #View #LinearLayout #appCafe 
### Основные понятия
**

>[!warning ] `ScrollView` — это `View-группа`, у которой есть особенность: в нее можно положить только один элемент, обычно, это `View-группы`, например, [[LinearLayout]]; благодаря ему у экрана появляется возможность пролистывания. 

>[!success ] Он занимает весь экран и по этой причине `View-группы` должны занимать длину столько, сколько ему надо, а не весь экран. 

>[! ] Он может быть не только корневой элементом (если он таки является корневым, то вы должны скопировать `xmlns` у предыдущего корневого `View-элемента`), но и также быть просто родитель для одного элемента, находясь в корневом элементе.
### Примеры использования:

```xml
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"  
    android:layout_width="match_parent"  
    android:layout_height="match_parent">  
  
    <LinearLayout        android:id="@+id/main"  
        android:layout_width="match_parent"  
        android:layout_height="wrap_content"  
        android:orientation="vertical">  
  
        <TextView            android:layout_width="wrap_content"  
            android:layout_height="wrap_content"  
            android:layout_margin="24dp"  
            android:text="@string/name"  
            android:textSize="48sp" />  
  
        <TextView            android:id="@+id/tvName"  
            android:layout_width="wrap_content"  
            android:layout_height="wrap_content"  
            android:layout_margin="24dp"  
            android:textSize="48sp" />  
  
        <TextView            android:layout_width="wrap_content"  
            android:layout_height="wrap_content"  
            android:layout_margin="24dp"  
            android:text="@string/drink"  
            android:textSize="48sp" />  
  
        <TextView            android:id="@+id/tvDrinkName"  
            android:layout_width="wrap_content"  
            android:layout_height="wrap_content"  
            android:layout_margin="24dp"  
            android:textSize="48sp" />  
  
        <TextView            android:layout_width="wrap_content"  
            android:layout_height="wrap_content"  
            android:layout_margin="24dp"  
            android:text="@string/type_drink"  
            android:textSize="48sp" />  
  
        <TextView            android:id="@+id/tvDrinkType"  
            android:layout_width="wrap_content"  
            android:layout_height="wrap_content"  
            android:layout_margin="24dp"  
            android:textSize="48sp" />  
  
        <TextView            android:layout_width="wrap_content"  
            android:layout_height="wrap_content"  
            android:layout_margin="24dp"  
            android:text="@string/tv_additives"  
            android:textSize="48sp" />  
  
        <TextView            android:id="@+id/tv_additives"  
            android:layout_width="wrap_content"  
            android:layout_height="wrap_content"  
            android:layout_margin="24dp"  
            android:textSize="48sp" />  
  
    </LinearLayout>
</ScrollView>
```


