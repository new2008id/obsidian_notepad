#multithreading #java 
### Основные понятия

>[!warning ] У наследоваться от класса `Thread`.

>[!success ] Реализовать интерфейс `Runnable`. (**Данный способ предпочтительнее**), т.к запрещено множественное наследования
### Примеры использования:

Запуск потока происходит через метод - `start()`

```java
public class Main {  
    public static void main(String[] args) {  
        System.out.println("Start");  
        MyRunnable myRunnable = new MyRunnable();  
        Thread myThread = new Thread(new Runnable() {  
            @Override  
            public void run() {  
                for (int i = 0; i < 1000; i++) {  
                    System.out.print(i);  
                }  
            }  
        });  
        myThread.start();  
  
        for (int i = 0; i < 1000; i++) {  
            System.out.print("M");  
        }  
        System.out.println("\nFinish");  
    }  
}
```


