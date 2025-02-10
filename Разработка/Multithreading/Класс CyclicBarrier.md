#multithreading #java #Thread #CyclicBarrier
### Основные понятия

`CyclicBarrier` (циклический барьер) - это класс в Java, который позволяет группе потоков ждать друг друга, пока все потоки не достигнут определенной точки в своем выполнении (барьера). Когда последний поток достигает барьера, барьер “срабатывает”, и все потоки продолжают выполнение.
### Конструкторы:

- `CyclicBarrier(int parties)`: Создает барьер для заданного количества потоков.
- `CyclicBarrier(int parties, Runnable barrierAction)`: Создает барьер для заданного количества потоков и задает действие барьера.
### Применение:

- `await()`: Ждет, пока все потоки не достигнут барьера. Возвращает индекс текущего потока, прибывшего к барьеру.
- `await(long timeout, TimeUnit unit)`: Ждет в течение заданного времени.
- `reset()`: Сбрасывает барьер в исходное состояние. Полезно, если один или несколько потоков прерваны или тайм-аут истек.
- `getParties()`: Возвращает количество потоков, необходимых для срабатывания барьера.
- `getNumberWaiting()`: Возвращает количество потоков, ожидающих у барьера.
- `isBroken()`: Возвращает true, если барьер сломан (например, из-за прерывания потока).
### Примеры использования:

```java
public class Main {  
    public static void main(String[] args) {  
//        CountDownLatch countDownLatch = new CountDownLatch(2);  
        CyclicBarrier cyclicBarrier = new CyclicBarrier(2);  
  
        for (int i = 0; i < 10; i++) {  
            new Thread(new Runnable() {  
                @Override  
                public void run() {  
                    long millis = (long) (Math.random() * 5000 + 1000);  
                    String name = Thread.currentThread().getName();  
                    System.out.println(name + ": Data is being prepared");  
                    try {  
                        Thread.sleep(millis);  
                        System.out.println(name + ": Data is ready");  
                    } catch (InterruptedException e) {  
                        e.printStackTrace();  
                    }  
                    try {  
                        cyclicBarrier.await();  
                    } catch (Exception e) {  
                        throw new RuntimeException(e);  
                    }  
                    System.out.println(name + ": Continue work");  
                }  
            }).start();  
        }  
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
```


