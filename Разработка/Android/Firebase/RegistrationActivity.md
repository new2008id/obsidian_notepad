#LinearLayout #Firebase #ScrollView #View 
### Дополнительные сведения о ScrollView и LinearLayout

Если вам нужно использовать `LinearLayout` и указать элементы, чтобы располагались в середине, достаточно использовать параметр `gravity=«center»`. Но если `LinearLayout` находится в `ScrollView`, то он займет столько, сколько ему нужно (то бишь из-за wrap_content будет занимать столько, сколько `View-элементов`). Для того, чтобы он занял всё место, нужно разрешить `ScrollView`, чтобы он занял всё свободное пространство на экране через параметр — `android:fillViewport="true"`
### Примеры использования:

*activity_registration.xml*
```xml
<ScrollView xmlns:app="http://schemas.android.com/apk/res-auto"  
    xmlns:tools="http://schemas.android.com/tools"  
    xmlns:android="http://schemas.android.com/apk/res/android"  
    android:id="@+id/main"  
    android:layout_width="match_parent"  
    android:layout_height="match_parent"  
    android:layout_marginStart="30dp"  
    android:layout_marginTop="50dp"  
    android:layout_marginEnd="30dp"  
    android:orientation="vertical"  
    android:fillViewport="true"  
    tools:context=".RegistrationActivity">
```



