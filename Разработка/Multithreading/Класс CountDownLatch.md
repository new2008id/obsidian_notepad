#multithreading 
### Основные понятия

`CountDownLatch` — это класс синхронизации, который позволяет одному или нескольким потокам ждать, пока не завершится определенное количество других операций, выполняемых другими потоками. Он работает как счетчик обратного отсчета.

>[! ] Есть следующая `задача`, требуется создать `10 потоков`, и вывести слово `Start - [index]`. В конце потока - `Finish - [index]`. После всех проделанных `операций`, вывести, `все потоки` завершили свою `работу`. 
### Примеры использования:

```java
public class Main {  
    public static void main(String[] args) {  
        List<Thread> threads = new ArrayList<>();  
        for (int i = 0; i < 10; i++) {  
            final int counter = i;  
            Thread thread = new Thread(new Runnable() {  
                @Override  
                public void run() {  
                    System.out.println("Start - " + counter);  
                    try {  
                        Thread.sleep(1000);  
                    } catch (InterruptedException e) {  
                        throw new RuntimeException(e);  
                    }  
                    System.out.println("Finish - " + counter);  
  
                }  
            });  
            threads.add(thread);  
            thread.start();  
        }  
  
        for (Thread thread : threads) {  
            try {  
                thread.join();  
            } catch (InterruptedException e) {  
                throw new RuntimeException(e);  
            }  
        }  
        System.out.println("All threads are terminated");  
    }  
}
```

>[!success ] Данный способ является слишком `длинным`, и поэтому для решения столь простой задачи, был разработан [[Класс CountDownLatch]]
#### С использованием [[Класс CountDownLatch]]

```java
public class Main {  
    public static void main(String[] args) {  
        CountDownLatch countDownLatch = new CountDownLatch(10);  
  
        for (int i = 0; i < 10; i++) {  
            final int counter = i;  
            new Thread(new Runnable() {  
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
            }).start();  
        }  
        try {  
            countDownLatch.await(); // wait for all threads to finish  
        } catch (InterruptedException e) {  
            throw new RuntimeException(e);  
        }  
        System.out.println("All threads are terminated");  
    }  
}
```

>[!warning ] Когда `счетчик` достигает нуля, все `потоки`, которые вызывали метод `await()`, `разблокируются` и продолжают свое выполнение.

>[!error ] Когда требуется выполнять множество различных задач в отдельных потоках, `используется` [[Класс ExcecutorService]]

### Применение

**Когда использовать `CountDownLatch`:**

- Когда нужно синхронизировать выполнение основного потока с несколькими другими потоками.
- Когда нужно дождаться, пока все потоки выполнят свою часть работы, прежде чем продолжить выполнение.
- Когда нужно запустить несколько потоков одновременно, но дождаться их завершения перед продолжением основной работы.
- Для выполнения подготовительных действий перед началом основной обработки.

**Преимущества `CountDownLatch`:**

- **Простота использования:** Легко понять и использовать в многопоточных приложениях.
- **Синхронизация:** Обеспечивает корректную синхронизацию потоков.
- **Гибкость:** Подходит для разных сценариев, где нужно дождаться завершения нескольких операций.

**Ограничения:**

- После того как счетчик достиг нуля, его нельзя сбросить (`переиспользовать`) для другого ожидания.
- Не подходит для циклического ожидания.
- Подходит только для одноразового ожидания, после того, как счетчик достиг нуля.