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