#parallelStream #java #stream 
### Основные понятия

Метод `parallelStream()` создает параллельный поток данных, один поток разбивается на несколько участков, операции над каждым участком выполняются одновременно,
после чего поток снова склеивается. Это позволяет некоторые операции делать быстрее.
### Примеры использования:

```java
public class Main {  
    public static void main(String[] args) {  
        List<Float> numbers = new ArrayList<>();  
        for (int i = 0; i < 30_000_000; i++) {  
            numbers.add((float) i);  
        }  
  
        long before = System.currentTimeMillis();  
        numbers.parallelStream()  
                .map((number) -> Math.sin(0.2f + number / 5) * Math.cos(0.2f + number / 5) * Math.cos(0.4f + number / 2))  
                .collect(Collectors.toList());  
  
        long after = System.currentTimeMillis();  
        System.out.println("Time: " + (after - before) + "ms");  
    }  
}
```

>[!success ] В данном примере показывается, как `parallelStream()`  ускоряет работу за счет создания параллельных потоков данных

