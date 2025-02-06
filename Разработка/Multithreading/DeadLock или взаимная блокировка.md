#multithreading #synchronized #monitor #Thread 
### Основные понятия

Deadlock — это ситуация, когда два или более потоков оказываются заблокированными навсегда, ожидая друг друга для освобождения ресурсов. Каждый поток удерживает ресурс, необходимый другому потоку для продолжения работы, и ни один из них не может освободить свои ресурсы, пока не получит чужой. В результате, все потоки оказываются в состоянии вечного ожидания.

### Условия возникновения Deadlock:

Для возникновения Deadlock должны одновременно выполняться четыре необходимых условия, известные как условия Коффмана (Coffman conditions):

1. **Взаимное исключение (Mutual Exclusion):** Как минимум один ресурс должен быть доступен в эксклюзивном режиме, то есть только один поток может владеть им в данный момент времени. Если ресурс разделяется между потоками, deadlock не возникнет.
    
2. **Удержание и ожидание (Hold and Wait):** Поток, уже удерживающий как минимум один ресурс, запрашивает дополнительный ресурс, который удерживается другим потоком. При этом поток не освобождает уже удерживаемые ресурсы.
    
3. **Отсутствие вытеснения (No Preemption):** Ресурс может быть освобожден только добровольно потоком, который им владеет, после завершения его использования. Невозможно принудительно отобрать ресурс у потока.
    
4. **Циклическое ожидание (Circular Wait):** Существует цепочка из двух или более потоков, каждый из которых ждет ресурс, удерживаемый следующим потоком в цепочке. Например, поток A ждет ресурс, удерживаемый потоком B, поток B ждет ресурс, удерживаемый потоком C, а поток C ждет ресурс, удерживаемый потоком A.

### Примеры использования:

```java
public class Account {  
    private int amount1;  
    private int amount2;  
    private final Object monitor1 = new Object();  
    private final Object monitor2 = new Object();  
  
    public Account(int amount1, int amount2) {  
        this.amount1 = amount1;  
        this.amount2 = amount2;  
    }  
  
    public void transferFrom1To2(int amount) {  
        synchronized (monitor1) {  
            try {  
                Thread.sleep(2000);  
            } catch (InterruptedException e) {  
                throw new RuntimeException(e);  
            }  
            if (amount <= amount1) {  
                System.out.println("amount <= amount1");  
                synchronized (monitor2) {  
                    try {  
                        Thread.sleep(2000);  
                    } catch (InterruptedException e) {  
                        throw new RuntimeException(e);  
                    }  
                    amount2 += amount;  
                    amount1 -= amount;  
                }  
            } else {  
                System.out.println("Not enough money in account 1");  
            }  
        }  
    }  
  
    public void transferFrom2To1(int amount) {  
        synchronized (monitor2) {  
            try {  
                Thread.sleep(2000);  
            } catch (InterruptedException e) {  
                throw new RuntimeException(e);  
            }  
            if (amount <= amount2) {  
                System.out.println("amount <= amount2");  
                synchronized (monitor1) {  
                    try {  
                        Thread.sleep(2000);  
                    } catch (InterruptedException e) {  
                        throw new RuntimeException(e);  
                    }  
                    amount2 -= amount;  
                    amount1 += amount;  
                }  
            } else {  
                System.out.println("Not enough money in account 1");  
            }  
        }  
    }   
}

public class Main {  
    public static void main(String[] args) {  
        Account account = new Account(1000, 1000);  
        new Thread(new Runnable() {  
            @Override  
            public void run() {  
                account.transferFrom1To2(300);  
            }  
        }).start();  
  
        new Thread(new Runnable() {  
            @Override  
            public void run() {  
                account.transferFrom2To1(500);  
            }  
        }).start();  
    }  
}
```


 