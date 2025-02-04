#multithreading #java #Runnable #anonymous_class
### Основные понятия

>[! ] `Многопоточность` - это средство, которое позволяет выполнять разные задачи одновременно.

 >[!warning ] `Многопоточность` на основе процессов - дает возможность разным программам или процессам работать параллельно.

>[!success ] `Многопоточность` на основе потоков - дает возможность выполнять одновременно несколько задач в рамках одной программы
### Применение:

#### 1-й способ использовать многопоточность - extends class Thread

```java
// первый способ реализации многопоточности, наследоваться от класса Thread  
public class MyThread extends Thread {  
    // код, который пишется в другом потоке, пишется в методе run()  
    @Override  
    public void run() {  
        for (int i = 0; i < 1000; i++) {  
            System.out.print(i);  
        }  
    }  
}

public class Main {  
    public static void main(String[] args) {  
        System.out.println("Start");  
        Thread myThread = new MyThread();  
        myThread.start();  
  
        for (int i = 0; i < 1000; i++) {  
            System.out.print("M");  
        }  
        System.out.println("\nFinish");  
    }  
}
```

#### 2-й способ использовать многопоточность - use interface Runnable()

```java
// второй способ реализации многопоточности, реализовать interface Runnable  
public class MyRunnable implements Runnable {  
    // код, который пишется в другом потоке, пишется в методе run()  
    @Override  
    public void run() {  
        for (int i = 0; i < 1000; i++) {  
            System.out.print(i);  
        }  
    }  
}

public class Main {  
    public static void main(String[] args) {  
        System.out.println("Start");  
        MyRunnable myRunnable = new MyRunnable();  
        Thread myThread = new Thread(myRunnable);  
        myThread.start();  
  
        for (int i = 0; i < 1000; i++) {  
            System.out.print("M");  
        }  
        System.out.println("\nFinish");  
    }  
}
```

Также можно использовать [[Анонимные классы]] для реализации `interface Runnable`

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

[[Cпособы создания потоков бывают]]



