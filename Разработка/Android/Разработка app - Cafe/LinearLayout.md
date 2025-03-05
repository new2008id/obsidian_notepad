#android #LinearLayout #appCafe 
### Основные понятия

`LinearLayout` - это один из базовых и наиболее часто используемых макетов в Android для организации пользовательского интерфейса. Он позволяет размещать дочерние элементы (виджеты и другие макеты) либо по горизонтали, либо по вертикали.

- **Ориентация:**
    - `android:orientation="horizontal"` - Элементы располагаются друг за другом слева направо.
    - `android:orientation="vertical"` - Элементы располагаются друг под другом сверху вниз. Это ориентация по умолчанию.

По умолчанию создания макета используется View-группа ConstraintLayout. Особенность его заключается в том, что нужно конкретно указывать layout_constraint у каждого View-элемента в зависимости экрана или от других View-элементов, иначе будет ошибка. 

Но если нам нужно, чтобы View-элементы были друг за другом вертикально или горизонтально, используется иной View-группа — LinerLayout. Ему ненужно указывать constraints для каждой элементов, он и так располагает их друг за другом.**
### Примеры использования:

```xml 
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"  
    xmlns:app="http://schemas.android.com/apk/res-auto"  
    xmlns:tools="http://schemas.android.com/tools"  
    android:id="@+id/main"  
    android:layout_width="match_parent"  
    android:layout_height="match_parent"  
    android:orientation="vertical"  
    tools:context=".MainActivity">  
  
    <ImageView        android:id="@+id/imageViewLogo"  
        android:layout_width="match_parent"  
        android:layout_height="0dp"  
        android:layout_weight="1"  
        android:adjustViewBounds="true"  
        android:contentDescription="@string/logo"  
        android:padding="36dp"  
        app:srcCompat="@drawable/dunkin_donuts" />  
  
    <TextView        android:id="@+id/welcome"  
        android:layout_width="match_parent"  
        android:layout_height="wrap_content"  
        android:padding="16dp"  
        android:text="@string/welcome"  
        android:textAlignment="center"  
        android:textColor="@color/purple_500"  
        android:textSize="24sp"  
        android:textStyle="bold" />  
  
    <EditText        android:id="@+id/etUsername"  
        android:layout_width="match_parent"  
        android:layout_height="wrap_content"  
        android:layout_margin="24dp"  
        android:autofillHints=""  
        android:hint="@string/username_hint"  
        android:inputType="textCapWords"  
  
        />  
  
    <EditText        android:id="@+id/etPassword"  
        android:layout_width="match_parent"  
        android:layout_height="wrap_content"  
        android:layout_marginStart="24dp"  
        android:layout_marginTop="0dp"  
        android:layout_marginEnd="24dp"  
        android:layout_marginBottom="24dp"  
        android:autofillHints=""  
        android:hint="@string/password_hint"  
        android:inputType="textPassword" />  
  
    <Button        android:id="@+id/buttonSignIn"  
        android:layout_width="match_parent"  
        android:layout_height="wrap_content"  
        android:layout_marginStart="24dp"  
        android:layout_marginTop="0dp"  
        android:layout_marginEnd="24dp"  
        android:layout_marginBottom="24dp"  
        android:text="@string/log_in" />  
  
</LinearLayout>
```

Если нужно загрузить изображение в приложении, то используется папка [[Drawable и ImageView]]
