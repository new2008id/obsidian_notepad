#Firebase #Shape #Rectangle #Corners #Solid
### Основные понятия

##### Делаем скругленный квадрат

Для того, чтобы сделать скругленный квадрат, используется `shape`. Нам нужен именно квадрат, для этого используется параметр в `solid` «`rectangle`». Теперь нам нужно добавить скругление, для этого используется новый параметр — `corners`. С помощью радиусов мы указываем, насколько должно быть скруглены края.

```xml
<?xml version="1.0" encoding="utf-8"?>  
<shape xmlns:android="http://schemas.android.com/apk/res/android"  
    android:shape="rectangle">  
    <solid android:color="#9CF5E5" />  
    <corners        android:radius="16dp"  
        android:topRightRadius="0dp" />  
    <padding        android:bottom="12dp"  
        android:left="12dp"  
        android:right="12dp" />  
  
</shape>
```

![[Pasted image 20250402100003.png]]

