#android #LinearLayout #drawable #ImageView #View #EditText #Button #appCafe 
### Основные понятия

Если нужно загрузить изображение в приложении, то используется папка `Drawable`. Однако, рекомендуется использовать изображения в формате `svg` или `png`, иначе будет плохое качество у какого-то устройства. Для того, чтобы загрузить изображение, выполните следующие действия:
- Нажмите на эту папку правой кнопки мышки, дальше «`New`» и выберете «`Vector Image`»
- Выбирайте «`Local file`» и ищите нужный файл
- `Next` и `Finish`

>[! ] Для того, чтобы использовать изображение, используется `ImageView`.
### Применение:

Однако, бывает, что изображение занимает всё пространство. Чтобы такого не было, используется `adjustViewBounds` (настроить границы `View`-элемента), он занимает столько, сколько действительно нужно для изображения и в соответствии размеру компонента-контейнера.
##### Свойство layout_weight

Если нужно, чтобы какой-то `View`-элемент занял всё свободное пространство или пропорционально с другим, или один элемент больше, а другой меньше, — используется `layout_weight=«Number»`. Прежде использовать, нужно указать `0dp` у `layout_width` или у `layout_height`. 

##### Пример работы `layout_weight`
```xml
<ImageView  
    android:id="@+id/imageViewLogo"  
    android:layout_width="match_parent"  
    android:layout_height="0dp"  
    android:layout_weight="1"  
    android:adjustViewBounds="true"  
    android:contentDescription="@string/logo"  
    android:padding="36dp"  
    app:srcCompat="@drawable/dunkin_donuts" />
```

#### *Полезное*

- Чтобы текст начался с большой буквы в `Edittext`, используется `android:inputType="textCapWords`"
- Чтобы вместо букв были кружочки (пароль), нужно использовать `android:inputType="textPassword"`
#### *Замечание*

- `contentDescription()` — это строка отвечает за чтения изображения для слепых и для слабовидящих. Если вы планируете публиковать приложение, то обязательно нужно указать текст, который описывает изображение, данный текст будет озвучен приложений. Если не планируете, то просто добавьте `@null`, чтобы убрать предупреждение.
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
  
    <ImageView android:id="@+id/imageViewLogo"  
        android:layout_width="match_parent"  
        android:layout_height="0dp"  
        android:layout_weight="1"  
        android:adjustViewBounds="true"  
        android:contentDescription="@string/logo"  
        android:padding="36dp"  
        app:srcCompat="@drawable/dunkin_donuts" />  
  
    <TextView android:id="@+id/welcome"  
        android:layout_width="match_parent"  
        android:layout_height="wrap_content"  
        android:padding="16dp"  
        android:text="@string/welcome"  
        android:textAlignment="center"  
        android:textColor="@color/purple_500"  
        android:textSize="24sp"  
        android:textStyle="bold" />  
  
    <EditText android:id="@+id/etUsername"  
        android:layout_width="match_parent"  
        android:layout_height="wrap_content"  
        android:layout_margin="24dp"  
        android:autofillHints=""  
        android:hint="@string/username_hint"  
        android:inputType="textCapWords"  
  
        />  
  
    <EditText android:id="@+id/etPassword"  
        android:layout_width="match_parent"  
        android:layout_height="wrap_content"  
        android:layout_marginStart="24dp"  
        android:layout_marginTop="0dp"  
        android:layout_marginEnd="24dp"  
        android:layout_marginBottom="24dp"  
        android:autofillHints=""  
        android:hint="@string/password_hint"  
        android:inputType="textPassword" />  
  
    <Button android:id="@+id/buttonSignIn"  
        android:layout_width="match_parent"  
        android:layout_height="wrap_content"  
        android:layout_marginStart="24dp"  
        android:layout_marginTop="0dp"  
        android:layout_marginEnd="24dp"  
        android:layout_marginBottom="24dp"  
        android:text="@string/log_in" />  
  
</LinearLayout>
```
