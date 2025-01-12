## Основные понятия

>[! ] **Handler** - это инструмент для отправки сообщений в эту очередь Looper и обработки их в соответствующем потоке.  

>[!error ] Looper -  это “сердце” потока, который обрабатывает очередь сообщений.

### Примеры использования

Для начала требуется инициализировать Handler - и можно его использовать в основном потоке. Можно инициализировать различными способами:
1. 
```kotlin
// обработка сообщений в основном потоке
Handler(Looper.getMainLooper())
```

2. 
```kotlin
// обработка сообщений на потоке вызова перед созданием, обязательно нужен вызов
// Looper.prepare()
Handler(Looper.myLooper())
```

### Советы использования 
- Handler-y можно передавать сообщения типa Runnable или Message
- Передача Runnable - post(Runnable) или postDelayed(Runnable, long delay)
- Передача Message - sendMessage(Message) или sendMessageDelayed(Message, long delay)
- Чтобы обрабатывать объекты Message, нужно у наследоваться от Handler и переопределить метод handleMessage()
- Объекты типа Runnable явно обрабатывать не нужно, у них будет вызван метод run()

### Измененный код с использованием [[Handler и Looper]]
```kotlin
private fun loadCity(callback: (String) -> Unit) {  
    thread {  
        Thread.sleep(5000)  
        runOnUiThread {  
            callback.invoke("Moscow")  
        }  
    }}
```

```kotlin
private fun loadTemperature(city: String, callback: (Int) -> Unit) {  
        thread {  
            runOnUiThread {  
                Toast.makeText(  
                    this,  
                    "Loading temperature for this $city",  
                    Toast.LENGTH_SHORT  
                ).show()  
            }  
  
//            Handler(Looper.getMainLooper()).post {  
//                Toast.makeText(  
//                    this,  
//                    "Loading temperature for this $city",  
//                    Toast.LENGTH_SHORT  
//                ).show()  
//            }  
            Thread.sleep(5000)  
  
            runOnUiThread {  
                callback.invoke(17)  
            }  
//            Handler(Looper.getMainLooper()).post {  
//                callback.invoke(17)  
//            }  
        }  
    }
```

>[!warning] `runOnUiThread{}` - это, по сути, сокращенная запись для `Handler().post{}` с использованием `Looper.getMainLooper()`

Данный подход с использованием callback называется - [[Callback Hell]]. У данного подхода есть [[Проблемы при стандартном подходе к асинхронному программированию]]