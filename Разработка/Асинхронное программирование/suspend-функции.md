### Основные понятия

>[!warning] **Suspend function в Kotlin** — это **функция, которая может приостановить своё выполнение и возобновить его через некоторый период времени**.

### Примеры использования

```kotlin
suspend fun download(url: String): File {
    networkService.download(url, object: NetworkService.Callback {
        override fun onSuccess(result: File) {
        }
    })
}

private suspend fun loadCity(): String {  
        delay(5000)  
        return "Moscow"  
    }  

private suspend fun loadTemperature(city: String): Int {  
            this,  
            "Loading temperature for city: $city",  
            Toast.LENGTH_SHORT  
        ).show()  
        delay(5000)  
        return 17  
    }
```

Метод **delay()** устанавливает задержку на 5 секунд, при этом, сам поток не блокируется, после чего выполняется следующие код.

>[!error] `Suspend` функции никогда не должны блокировать поток, модификатор `suspend` не говорит о том, что поток не может быть заблокирован

>[! ] Исключениями являются, библиотеки `Retrofit` или `Room`, где данная возможность ПОДДЕРЖИВАЕТСЯ

### Примеры блокировки потока
```kotlin
private suspend fun loadCity(): String {  
	Thread.sleep(5000)  
	return "Moscow"  
}
```

>[!warning ] При написании своей `suspend` функции, нужно сделать так, чтобы она не блокировала поток

### Правильная обработка от блокировки потока
```kotlin
private suspend fun loadCity(): String {  
	delay(5000)
	return "Moscow"  
}
```