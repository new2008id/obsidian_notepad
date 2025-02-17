#multithreading #synchronized #join
### Основные понятия

Создать класс `Банкомат`, в котором изначально есть какая-то сумма денег. Создать `метод`, который выводит деньги со счета. В качестве `параметра` этот `метод` принимает `имя человека`, который выводит `деньги` и `сумму`, которую он хочет вывести.

Последовательность действий внутри метода:
1. Выводится строка «`Имя` подошел к банкомату»
2. Поток останавливается на `2 секунды`
3. Осуществляется проверка - если в банкомате достаточно денег для выдачи, то выводится строка - `Имя вывел сумма рублей. В банкомате осталось оставшаяся сумма рублей`.
Если же в банкомате недостаточно денег, то выводится строка - `"В банкомате недостаточно денег для имя"`, 
В методе `main` создайте несколько `потоков`, каждый из которых будет представлять собой клиента, который хочет вывести деньги. 
Намеренно сделайте так, что кому-то из них не хватит денег и запустите код на выполнение.

Из-за отсутствия синхронизации у вас может возникнуть проблема — `состояние гонки`, После того, как деньги закончились, кто-то
еще смог их вывести и в банкомате осталась отрицательная сумма. Когда убедитесь, что проблема есть, решите ее двумя способами:
1. Без синхронизации. При помощи [[Метод join]] - пусть каждый поток ждет, пока закончит предыдущий и потом приступает к
работе.
2. С помощью синхронизации. Синхронизируйте метод, используя в качестве монитора this, а потом сделайте тоже самое используя свой созданный объект синхронизации.

>[!warning ] В каждом случае проверяйте код на работоспособность.

### Примеры использования:

#### Способ использование join()

```java
public class CashDispenser {  
    private int balance;   
  
    public CashDispenser(int balance) {  
        this.balance = balance;  
    }  
  
    public void withdraw(String name, int amount) {  
        System.out.println(name + " went to the ATM");  
        try {  
            Thread.sleep(2000);  
        } catch (InterruptedException e) {  
            throw new RuntimeException(e);  
        }  
        if (amount > balance) {  
            System.out.println("There is not enough money in the ATM for " + name);  
        } else {  
            balance -= amount;  
            System.out.println(name + " withdrawn " + amount + " rubles." + " There are: " + balance + " rubles left in the ATM");  
        }   
    }  
}
```

```java
public class Main {  
    public static void main(String[] args) {  
        CashDispenser cashDispenser = new CashDispenser(5000);  
 
        // вариант решения с join()        
		Thread thread1 = new Thread(new Runnable() {  
            @Override  
            public void run() {  
                cashDispenser.withdraw("Denis", 500);  
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
                cashDispenser.withdraw("Nastya", 250);  
            }  
        });  
  
        Thread thread3 = new Thread(new Runnable() {  
            @Override  
            public void run() {  
                try {  
                    thread2.join();  
                } catch (InterruptedException e) {  
                    throw new RuntimeException(e);  
                }  
                cashDispenser.withdraw("Olga", 250);  
            }  
        });  
  
        Thread thread4 = new Thread(new Runnable() {  
            @Override  
            public void run() {  
                try {  
                    thread3.join();  
                } catch (InterruptedException e) {  
                    throw new RuntimeException(e);  
                }  
                cashDispenser.withdraw("Dmitriy", 1250);  
            }  
        });  
  
        Thread thread5 = new Thread(new Runnable() {  
            @Override  
            public void run() {  
                try {  
                    thread4.join();  
                } catch (InterruptedException e) {  
                    throw new RuntimeException(e);  
                }  
                cashDispenser.withdraw("Oleg", 5250);  
            }  
        });  
  
        thread1.start();  
        thread2.start();  
        thread3.start();  
        thread4.start();  
        thread5.start();  
  
    }  
}
```

#### 2-й способ решения задачи с использованием synchronized

```java
public class CashDispenser {  
    private int balance;  
    private final Object monitor = new Object();  
  
    public CashDispenser(int balance) {  
        this.balance = balance;  
    }  
  
    public void withdraw(String name, int amount) {  
        synchronized (monitor) {  
            System.out.println(name + " went to the ATM");  
            try {  
                Thread.sleep(2000);  
            } catch (InterruptedException e) {  
                throw new RuntimeException(e);  
            }  
            if (amount > balance) {  
                System.out.println("There is not enough money in the ATM for " + name);  
            } else {  
                balance -= amount;  
                System.out.println(name + " withdrawn " + amount + " rubles." + " There are: " + balance + " rubles left in the ATM");  
            }  
        }  
    }  
}
```

```java
public class Main {  
    public static void main(String[] args) {  
        CashDispenser cashDispenser = new CashDispenser(5000);  
  
//      вариант решения с синхронизацией  
        Thread thread1 = new Thread(() -> cashDispenser.withdraw("Denis", 500));  
        Thread thread2 = new Thread(() -> cashDispenser.withdraw("Nastya", 250));  
        Thread thread3 = new Thread(() -> cashDispenser.withdraw("Olga", 500));  
        Thread thread4 = new Thread(() -> cashDispenser.withdraw("Dmitriy", 1250));  
        Thread thread5 = new Thread(() -> cashDispenser.withdraw("Oleg", 5250));   
  
        thread1.start();  
        thread2.start();  
        thread3.start();  
        thread4.start();  
        thread5.start();  
    }  
}
```