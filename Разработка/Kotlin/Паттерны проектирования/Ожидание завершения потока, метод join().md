#join #Thread 
### Основные понятия

Метод `join()` позволяет одному потоку ждать завершения другого потока. Когда поток вызывает `join()` на другом потоке, он блокируется до тех пор, пока другой поток не завершит свое выполнение.
### Применение:

```kotlin
import kotlin.concurrent.thread

fun main() {
    val thread = thread {
        Thread.sleep(2000L) // Поток спит 2 секунды
        println("Thread finished")
    }

    println("Waiting for thread to finish")
    thread.join() // Блокируем основной поток до завершения thread
    println("Main thread continues")
}
```

>[! success ] В этом примере основной поток вызывает `thread.join()`, поэтому он блокируется и ждет, пока поток `thread` не завершит свое выполнение. После завершения `thread`, основной поток продолжает выполнение.

