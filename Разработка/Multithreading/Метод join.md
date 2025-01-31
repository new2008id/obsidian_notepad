#java #multithreading 
### Основные понятия

- **Назначение:** Метод `join()` позволяет одному потоку дождаться завершения другого потока.
- **Действие:** Когда поток вызывает метод `join()` для другого потока, вызывающий поток приостанавливает своё выполнение, пока целевой поток не завершится.
- Метод `join()` может выбрасывать исключение `InterruptedException`.
- Перегруженные версии метода `join()` позволяют указать максимальное время ожидания
- Данный метод также нужно оборачивать в блок `try/catch`

### Примеры использования:

```java
public class Main {  
    private static List<String> list;  
  
    public static void main(String[] args) throws InterruptedException {  
        List<Integer> list1 = new ArrayList<>();  
        List<Integer> list2 = new ArrayList<>();  
        List<Integer> list3 = new ArrayList<>();  
  
        Thread thread1 = new Thread(new Runnable() {  
            @Override  
            public void run() {  
                for (int i = 0; i < 1_000_000; i++) {  
                    list1.add(i);  
                }  
            }  
        });  
  
        Thread thread2 = new Thread(new Runnable() {  
            @Override  
            public void run() {  
                for (int i = 0; i < 1_000_000; i++) {  
                    list2.add(i);  
                }  
            }  
        });  
  
        Thread thread3 = new Thread(new Runnable() {  
            @Override  
            public void run() {  
                for (int i = 0; i < 1_000_000; i++) {  
                    list3.add(i);  
                }  
            }  
        });  
  
        thread1.start();  
        thread2.start();  
        thread3.start();  
        // join заставляет поток, в котором вызван метод, ждать, пока не завершится поток, в котором вызван метод  
        // метод join нужно обернуть в try/catch        thread1.join();  
        thread2.join();  
        thread3.join();  
        System.out.println(list1.size());  
        System.out.println(list2.size());  
        System.out.println(list3.size());  
    }  
}
```
### Другой пример...

```java
public class Main {  
    private static List<String> list;  
  
    public static void main(String[] args) throws InterruptedException {  
        Thread thread1 = new Thread(new Runnable() {  
            @Override  
            public void run() {  
                System.out.println(1);  
            }  
        });  
  
        Thread thread2 = new Thread(new Runnable() {  
            @Override  
            public void run() {  
                System.out.println(2);  
            }  
        });  
  
        Thread thread3 = new Thread(new Runnable() {  
            @Override  
            public void run() {  
                System.out.println(3);  
            }  
        });  
  
        thread1.start();  
        thread2.start();  
        thread3.start();  
    }  
}
```

В данном примере, ожидаем, что произойдет вывод по порядке, 1, 2, 3. Но, по факту, вывод будет осуществляться всегда по разному 

```java 
> Task :Main.main()
2
3
1
``` 

>[!warning ] Здесь стоит знать, если был создан поток и сразу же запущен, то точно неизвестно, когда он точно будет запущен, никогда нельзя знать порядок, в котором будут запускаться потоки. 

>[! ] Даже если потоки были запущены по очереди, как в примере выше, то это не значит, что данные потоки будут выполнятся в данном порядке. 

>[!success ] Происходит это потому, что на поток нужно определенное количество времени. Один поток, может быть построен раньше, другой позже и т.д.

```java
public class Main {  
    private static List<String> list;  
  
    public static void main(String[] args) throws InterruptedException {  
        Thread thread1 = new Thread(new Runnable() {  
            @Override  
            public void run() {  
                list = new ArrayList<>();  
            }  
        });  
  
        Thread thread2 = new Thread(new Runnable() {  
            @Override  
            public void run() {  
                try {  
                    thread1.join();  
                } catch (InterruptedException e) {  
                    throw new RuntimeException(e);  
                }  
                System.out.println(list.size());  
            }  
        });  
  
        thread1.start();  
        thread2.start();  
    }  
}
```

>[! ] В данном примере показана инициализация массива и вывод его размера в разных потоках. Если не использовать [[Метод join]], то лишь иногда у переменной `list` будет выведен массив, т. к. точно неизвестно, за какой промежуток времени выполниться `thread1`, поэтому чтобы точно выполнить `thread2` без ошибок, лучше использовать [[Метод join]] и дождаться завершения `thread1`.

[[Практика по использованию многопоточности]] 