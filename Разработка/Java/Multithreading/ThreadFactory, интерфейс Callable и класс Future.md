#multithreading #ThreadFactory #Callable #Future
### Основные понятия

`ThreadFactory` — это интерфейс, который позволяет настраивать создание потоков. Он содержит всего один метод:

```java
Thread newThread(Runnable r);
```
- **Назначение:** Отделить логику создания и настройки потоков от логики выполнения задач.
- **Преимущества:**
    - Централизованное управление созданием потоков.
    - Настройка потоков (имя, приоритет, daemon mode).
    - Интеграция с `ExecutorService`.

`Callable` — это интерфейс, похожий на `Runnable`, но с двумя ключевыми отличиями:

- `Callable` может возвращать значение.
- `Callable` может выбрасывать исключения.

Интерфейс `Callable` содержит один метод:

```java
V call() throws Exception;
```
- **Назначение:** Представляет задачу, которая возвращает результат и может выбрасывать исключения.
- **Преимущества:**
    - Возвращение результата выполнения задачи.
    - Обработка исключений, возникающих в процессе выполнения задачи.

`Future` — это интерфейс, который представляет результат асинхронного вычисления. Он предоставляет методы для проверки, завершилось ли вычисление, получения результата и отмены вычисления.

Интерфейс `Future` содержит следующие основные методы:

- `boolean isDone()`: Проверяет, завершилось ли вычисление.
- `V get()`: Получает результат вычисления. Этот метод блокирует текущий поток до тех пор, пока результат не станет доступен.
- `V get(long timeout, TimeUnit unit)`: Получает результат вычисления с таймаутом.
- `boolean cancel(boolean mayInterruptIfRunning)`: Отменяет вычисление.

- **Назначение:** Получение результатов асинхронных задач, запущенных через `ExecutorService`.
    
- **Преимущества:**
    - Асинхронное получение результатов.
    - Проверка статуса выполнения задачи.
    - Отмена задачи.

### Применение:

1. **ThreadFactory:** Используется для создания потоков с определенными настройками. `ExecutorService` использует `ThreadFactory` для создания потоков в пуле.
    
2. **Callable:** Представляет задачу, которую нужно выполнить асинхронно.
    
3. **ExecutorService:** Принимает `Callable` объекты и запускает их на выполнение в пуле потоков. Метод `submit()` возвращает объект `Future`.
    
4. **Future:** Представляет результат асинхронного вычисления. Вы можете использовать `Future` для проверки статуса выполнения задачи, получения результата (блокируясь, если необходимо) или отмены задачи.

### Примеры использования:

```java
public class Main {  
    public static void main(String[] args) throws InterruptedException {  
        // для запуска timer  
        ExecutorService executorService = Executors.newFixedThreadPool(3, new ThreadFactory() {  
            @Override  
            public Thread newThread(Runnable r) {  
                Thread thread = new Thread(r);  
                thread.setDaemon(true);  
                return thread;  
            }  
        });  
        executorService.execute(new Runnable() {  
            @Override  
            public void run() {  
                try {  
                    while (true) {  
                        System.out.print(".");  
                        Thread.sleep(300);  
                    }  
                } catch (InterruptedException e) {  
                    throw new RuntimeException(e);  
                }  
            }  
        });  
  
        Future<String> futureName = executorService.submit(new Callable<String>() {  
            @Override  
            public String call() throws Exception {  
                try {  
                    Thread.sleep(5000);  
                } catch (InterruptedException e) {  
                    throw new RuntimeException(e);  
                }  
  
                return "John";  
            }  
        });  
        Future<Integer> futureAge = executorService.submit(new Callable<Integer>() {  
            @Override  
            public Integer call() throws Exception {  
                try {  
                    Thread.sleep(4000);  
                } catch (InterruptedException e) {  
                    throw new RuntimeException(e);  
                }  
  
                return 25;  
            }  
        });  
  
        try {  
            String name = futureName.get();  
            int age = futureAge.get();  
            System.out.println("\nName: " + name + ", Age: " + age);  
        } catch (ExecutionException e) {  
            throw new RuntimeException(e);  
        }  
  
//        Future<String> futureName = executorService.submit(new Runnable() {  
//            @Override  
//            public void run() {  
//                try {  
//                    Thread.sleep(5000);  
//                } catch (InterruptedException e) {  
//                    throw new RuntimeException(e);  
//                }  
//  
//                return "John";  
//            }  
//        });  
  
    }  
}
```


