### Условие задачи

Создать класс МФУ (многофункциональное устройство), которое умеет сканировать и печатать документы. У него должно быть 2 метода `print()` и `scan()`, которые в качестве параметра принимают количество страниц.

Если вы передали в метод `print()` число 3, выводить строки "Отпечатано 1 стр", потом "Отпечатано 2 стр", "Отпечатано 3 стр". Между выводами добавьте небольшую задержку. Метод `scan()` делает тоже самое, только вместо слова "Отпечатано" будет "Отсканировано".

Методы должны быть синхронизированы таким образом, чтобы можно было из разных потоков одновременно запустить сканирование и печать, но при этом нельзя одновременно сканировать или печатать несколько документов.
### Примеры использования:

```java
public class MFU {  
    private final Object lock1 = new Object();  
    private final Object lock2 = new Object();  
    private static final int DELAY = 1000;  
    private static final String PRINT = "Print";  
    private static final String SCAN = "Scan";  
  
    public void print(int count) {  
        generalMethod(count, PRINT, lock1);  
    }  
  
    public void scan(int count) {  
        generalMethod(count, SCAN, lock2);  
    }  
  
    private void generalMethod(int count, String action, Object generalLock) {  
        synchronized (generalLock) {  
            try {  
                for (int i = 1; i <= count; i++) {  
                    Thread.sleep(DELAY);  
                    System.out.println(action + ": " + i + " pages");  
                }  
            } catch (Exception e) {  
                Thread.currentThread().interrupt();  
                return;  
            }  
        }  
    }  
}

public class Main {  
    public static void main(String[] args) {  
        MFU mfu = new MFU();  
  
        new Thread(() -> mfu.print(10)).start();  
        new Thread(() -> mfu.scan(10)).start();  
  
    }  
}
```


