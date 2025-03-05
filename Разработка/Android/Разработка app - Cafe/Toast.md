#android #Toast #appCafe
### Основные понятия

Если вам нужно вывести всплывающее сообщение на экране пользователя, то используется метод `Toast.makeText().show()`. У него есть три параметра:

- `applicationContext` — экран, на котором будет выведен;
- `text` — текст, который будет выведен. Желательно выводить из строкового ресурса;
- `duration` — время отображения.
### Применение:

![[Pasted image 20250218130111.png]]
### Примеры использования:

```java
if (userName.isEmpty() || password.isEmpty()) {  
    Toast.makeText(  
            this,  
            R.string.error_fields_empty,  
            Toast.LENGTH_SHORT  
    ).show();  
} else {  
    launchMakeOrderActivity(userName);  
}
```


