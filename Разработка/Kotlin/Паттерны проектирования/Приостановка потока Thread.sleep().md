#Thread #kotlin 
### Основные понятия

Метод `Thread.sleep()` приостанавливает выполнение текущего потока на указанное количество миллисекунд. Во время приостановки поток не выполняет никаких действий и не потребляет ресурсы процессора.
### Применение:

```kotlin
import kotlin.concurrent.thread

fun main() {
    thread {
        println("Thread is starting")
        Thread.sleep(2000L) // Приостанавливаем поток на 2 секунды
        println("Thread finished")
    }

    println("Main thread continues immediately")
}
```

>[! success ] В этом примере поток, созданный с помощью `thread {}`, приостанавливается на 2 секунды. В течение этого времени основной поток продолжает свое выполнение.


