#multithreading #java #semaphore #excecutorService #Thread 
### Основные понятия

>[!success ] Класс [[Semaphore]] управляет доступом к общему ресурсу с помощью счетчика. 

>[!warning ] Если значение счетчика больше нуля - доступ разрешен, если равно нулю, то в доступе будет отказано

`Semaphore` (семафор) - это класс в Java, который используется для управления доступом к общему ресурсу. Он поддерживает счетчик, представляющий количество доступных разрешений (permits). Потоки могут запрашивать разрешение на доступ к ресурсу (уменьшая счетчик) и освобождать разрешение после использования ресурса (увеличивая счетчик). Если счетчик равен нулю, потоки, запрашивающие разрешение, блокируются до тех пор, пока другое поток не освободит разрешение.
### Применение:

- **Permits (Разрешения):** Целое число, представляющее количество доступных разрешений.
- **Acquire (Получить):** Метод, который запрашивает разрешение. Если разрешения доступны, счетчик уменьшается, и поток продолжает выполнение. Если разрешения отсутствуют, поток блокируется до тех пор, пока разрешение не станет доступным.
- **Release (Освободить):** Метод, который освобождает разрешение, увеличивая счетчик. Это может разблокировать поток, ожидающий разрешения.
### Конструкторы:

- `Semaphore(int permits)`: Создает семафор с заданным количеством разрешений.
- `Semaphore(int permits, boolean fair)`: Создает семафор с заданным количеством разрешений и флагом fair. Если fair равен true, семафор предоставляет разрешения потокам в порядке FIFO (первый пришел - первый обслужен).
### Примеры использования:

```java
public class Main {  
    public static void main(String[] args) {  
        ExecutorService executorService = Executors.newFixedThreadPool(10);  
        // Semaphore - принадлежит для ограничений доступа к какому-либо ресурсу.  
        Semaphore semaphore = new Semaphore(3);  
        for (int i = 0; i < 10; i++) {  
            executorService.execute(new Runnable() {  
                @Override  
                public void run() {  
                    String name = Thread.currentThread().getName();  
                    System.out.println(name + " is working thread");  
                    try {  
                        Thread.sleep(500);  
                    } catch (InterruptedException e) {  
                        throw new RuntimeException(e);  
                    }  
                    try {  
                        semaphore.acquire();  
                        workWithFileSystem();  
                    } catch (InterruptedException e) {  
                        throw new RuntimeException(e);  
                    } finally {  
                        semaphore.release();  
                    }  
                    System.out.println(name + " is finished thread");  
                }  
            });  
        }  
        executorService.shutdown();  
    }  
  
    private static void workWithFileSystem() {  
        String name = Thread.currentThread().getName();  
        System.out.println(name + " is working with the file system");  
        try {  
            Thread.sleep(1000);  
        } catch (InterruptedException e) {  
            throw new RuntimeException(e);  
        }  
        System.out.println(name + " is finished with the file system");  
    }  
}
```

Продолжить многопоточность - [[Класс CyclicBarrier]]

Также будет описано [[Домашнее задание по Semaphore, CyclicBarrier.]], там описывается задача про гонку.
