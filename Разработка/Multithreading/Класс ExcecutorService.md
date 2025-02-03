#multithreading 
### Основные понятия

`ExecutorService` — это интерфейс, который предоставляет абстракцию для выполнения задач асинхронно. Он управляет пулом потоков и позволяет отправлять ему задачи на выполнение. Вместо того, чтобы создавать новые потоки вручную, вы отправляете задачи в `ExecutorService`, а он сам заботится о том, как и когда эти задачи будут выполнены.

>[!warning ]  Изначально создаётся определенное `количество потоков`, к примеру - 5. Если нужно выполнить `определенную задачу`, то она отдаётся [[Класс ExcecutorService]], он смотрит, что `все потоки свободны` и отдаёт ему на выполнение одному из них. 

>[! ] Если было набросано 5 задач, то они все начнут выполняться, каждая в своём потоке. 

>[!success ] Теперь, если нужно будет `добавить задачу - 6`, то она окажется в `очереди`, пока не освободиться какой-либо `поток`. Как только освободиться один из них, то берется `задача` из очереди и `начинает выполняться`.  
### Примеры использования:

```java
public class Main {  
    public static void main(String[] args) {  
        CountDownLatch countDownLatch = new CountDownLatch(10);  
        ExecutorService executorService = Executors.newFixedThreadPool(5); 
    // interface, под который нужно подставить определенную реализацию  
  
        for (int i = 0; i < 10; i++) {  
            final int counter = i;  
            executorService.execute(new Runnable() {  
                @Override  
                public void run() {  
                    System.out.println("Start - " + counter);  
                    try {  
                        Thread.sleep(1000);  
                    } catch (InterruptedException e) {  
                        throw new RuntimeException(e);  
                    }  
                    System.out.println("Finish - " + counter);  
                    countDownLatch.countDown();  
                }  
            });  
        }  
        executorService.shutdown(); // с этого момента в него уже нельзя передавать новые задачи  
        try {  
            countDownLatch.await(); // wait for all threads to finish  
        } catch (InterruptedException e) {  
            throw new RuntimeException(e);  
        }  
        System.out.println("All threads are terminated");  
    }  
}
```
### Примеры использования `newSingleThreadExecutor()`:

```java
public class Main {  
    public static void main(String[] args) {  
        CountDownLatch countDownLatch = new CountDownLatch(10);  
        ExecutorService executorService = Executors.newSingleThreadExecutor();  
  
        for (int i = 0; i < 10; i++) {  
            final int counter = i;  
            executorService.execute(new Runnable() {  
                @Override  
                public void run() {  
                    System.out.println("Start - " + counter);  
                    try {  
                        Thread.sleep(1000);  
                    } catch (InterruptedException e) {  
                        throw new RuntimeException(e);  
                    }  
                    System.out.println("Finish - " + counter);  
                    countDownLatch.countDown();  
                }  
            });  
        }  
        executorService.shutdown(); 
        try {  
            countDownLatch.await(); // wait for all threads to finish  
        } catch (InterruptedException e) {  
            throw new RuntimeException(e);  
        }  
        System.out.println("All threads are terminated");  
    }  
}
```

`executorService.shutdown();` - **с этого момента в него уже нельзя передавать новые задачи**.

>[! ] Работает точно также, как `newFixedThreadPool`, но его `пул` состоит из `одного потока`, когда первая задача выполнена, то берется `следующая задача` из очереди и т.д.
### Примеры использования `newCachedThreadPool()`:

```java
public class Main {  
    public static void main(String[] args) {  
        CountDownLatch countDownLatch = new CountDownLatch(10);  
        ExecutorService executorService = Executors.newCachedThreadPool();
  
        for (int i = 0; i < 10; i++) {  
            final int counter = i;  
            executorService.execute(new Runnable() {  
                @Override  
                public void run() {  
                    System.out.println("Start - " + counter);  
                    try {  
                        Thread.sleep(1000);  
                    } catch (InterruptedException e) {  
                        throw new RuntimeException(e);  
                    }  
                    System.out.println("Finish - " + counter);  
                    countDownLatch.countDown();  
                }  
            });  
        }  
        executorService.shutdown(); 
        try {  
            countDownLatch.await(); // wait for all threads to finish  
        } catch (InterruptedException e) {  
            throw new RuntimeException(e);  
        }  
        System.out.println("All threads are terminated");  
    }  
}
```

>[!success ] Cоздаёт новые потоки по `мере необходимости`, когда ему подаётся задача, он смотрит, есть ли `свободные потоки`, если есть, то отдаёт задачу ему, если нет, то `создаёт новый поток`.  

>[!warning ] Причем после завершения `задачи`, этот `пул` - не уменьшается.  

>[!error ] Может привести к `утечке` ресурсов