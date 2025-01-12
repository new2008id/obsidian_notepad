### Определение

Toast - тип короткого появляющегося сообщения в Android, которое позволяет отобразить информацию пользователю о определенной операции в приложении.

#### Пример использования 

```kotlin
private fun printToast() {  
	Toast.makeText(  
		this,  
		"Loading temperature for this $city",  
		Toast.LENGTH_SHORT  
	).show()  
    }  
```
