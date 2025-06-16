### Основные понятия

`Kotlin` предоставляет удобную функцию-строитель `thread {}`, которая упрощает создание и запуск потоков. Она является более компактной альтернативой созданию `Thread` с лямбда-выражением.

```kotlin
import kotlin.concurrent.thread

fun main() {
    thread { // Функция-строитель thread
        println("Thread is running")
    }
}
```

Функция `thread {}` автоматически создает, запускает и возвращает объект `Thread`. Она делает код более читаемым и лаконичным. Ты также можешь задать имя потока:
```kotlin
import kotlin.concurrent.thread

fun main() {
    thread(start = true, name = "MyCustomThread") {
        println("Thread is running")
    }
}
```
### Примеры использования:

```kotlin
import kotlin.concurrent.thread  
  
class ThreadRunner {  
    fun runThreads(): Map<String, String> {  
        val threadInfo = mutableMapOf<String, String>()  
  
        threadInfo[Thread.currentThread().name] = "Главный поток, который управляет выполнением"  
        thread {  
            threadInfo[Thread.currentThread().name] = "Выполняет вычисления 1"  
        }.join()  
        thread {  
            threadInfo[Thread.currentThread().name] = "Выполняет вычисления 2"  
        }.join()  
        thread {  
            threadInfo[Thread.currentThread().name] = "Выполняет вычисления 3"  
        }.join()  
        return threadInfo  
    }  
}  
  
fun main() {  
    val threadRunner = ThreadRunner()  
    val threadInfo = threadRunner.runThreads()  
    println(threadInfo)  
}
```


