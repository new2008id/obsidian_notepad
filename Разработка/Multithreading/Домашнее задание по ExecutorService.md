#multithreading #excecutorService
### Основные понятия

Используя [[Класс ExcecutorService]] необходимо запустить на выполнение 3 задачи в
отдельных потоках:

1 - посчитать и вывести в консоль сумму всех четных чисел от 0 до 1 000 000

2 - посчитать и вывести в консоль сумму всех чисел, которые без остатка
делятся на 7 (также от 0 до 1 000 000)

3 - создать коллекцию из 1000 элементов. Заполнить ее случайными
значениями от 0 до 1000 и вывести в консоль количество четных чисел в этой
коллекции.

В главном потоке дождаться выполнения всех задач, используя CountDownLatch,
замерить время их выполнения и вывести в консоль результат. Сначала сделать
это, создав пул из трех потоков, потом из одного и сравнить результат.
### Примеры использования:

```java
public class Main {  
    public static void main(String[] args) throws InterruptedException {  
        CountDownLatch countDownLatch = new CountDownLatch(3);  
//        ExecutorService executorService = Executors.newFixedThreadPool(3);  
        ExecutorService executorService = Executors.newSingleThreadExecutor();  
        final int num = 1_000_000;  
  
        Runnable task1 = new Runnable() {  
            long sum = 0;  
            @Override  
            public void run() {  
                for (int i = 0; i < num; i++) {  
                    if (i % 2 == 0) {  
                        sum += i;  
                    }  
                }  
                System.out.println("Task1: " + sum);  
                countDownLatch.countDown();  
            }  
        };  
  
        Runnable task2 = new Runnable() {  
            long sum = 0;  
            @Override  
            public void run() {  
                for (int i = 0; i < num; i++) {  
                    if (i % 7 == 0) {  
                        sum += i;  
                    }  
                }  
                System.out.println("Task2: " + sum);  
                countDownLatch.countDown();  
            }  
        };  
  
        Runnable task3 = new Runnable() {  
            private final Random random = new Random();  
            private final List<Integer> numbers = new ArrayList<>(1000);  
  
            @Override  
            public void run() {  
                int count = 1000;  
                for (int i = 0; i < count; i++) {  
                    numbers.add(random.nextInt(0, 1001));  
                }  
                int evenCount = 0;  
                for (int number : numbers) {  
                    if (number % 2 == 0) {  
                        evenCount++;  
                    }  
                }  
                System.out.println("Task3: " + evenCount);  
                countDownLatch.countDown();  
            }  
        };  
  
        long beforeTime = System.currentTimeMillis();  
  
        executorService.execute(task1);  
        executorService.execute(task2);  
        executorService.execute(task3);  
  
        executorService.shutdown();  
        try {  
            countDownLatch.await();  
        } catch (InterruptedException e) {  
            throw new RuntimeException(e);  
        }  
  
        long afterTime = System.currentTimeMillis();  
        System.out.println("Other time: " + (afterTime - beforeTime) + " ms");  
    }  
}
```




