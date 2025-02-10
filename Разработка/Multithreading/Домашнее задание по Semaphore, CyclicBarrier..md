### Основные понятия

Создать гонку, в которой каждый поток будет автомобилем.
Каждому автомобилю нужно:
1. Подготовиться к гонке.
2. Проехать участок обычной дороги.
3. Проехать через тоннель.
4. Проехать участок обычной дороги.
При этом должны быть выполнены следующие условия:
5. Всего участников 10.
6. У каждой машины разное время на подготовку к заезду, но стартовать они должны одновременно.
7. В тоннеле одновременно могут ехать только 3 машины.
8. Когда все 10 автомобилей закончат заезд, нужно вывести номер победителя и затраченное им время и список всех автомобилей с результатами заезда.
9. У каждой машины должно быть свое случайное время, за которое она готовится к гонке и за которое проезжает каждый из маршрутов.
### Примеры использования:

```java
public class Main {  
    private static final int NUMBER_OF_CARS = 10;  
    private static final int TUNNEL_CAPACITY = 3;  
    private static final Semaphore tunnelSemaphore = new Semaphore(TUNNEL_CAPACITY);  
    private static final ExecutorService executorService = Executors.newCachedThreadPool();  
    private static final CyclicBarrier cyclicBarrier = new CyclicBarrier(NUMBER_OF_CARS);  
    private static final Map<Integer, Long> score = new ConcurrentHashMap<>();  
    private static final CountDownLatch countDownLatch = new CountDownLatch(NUMBER_OF_CARS);  
    private static int winnerIndex = -1;  
    private static final Object monitor = new Object();  
  
    public static void main(String[] args) {  
        for (int i = 0; i < NUMBER_OF_CARS; i++) {  
            final int index = i;  
            executorService.execute(new Runnable() {  
                @Override  
                public void run() {  
                    prepare(index);  
                    try {  
                        cyclicBarrier.await();  
                    } catch (InterruptedException e) {  
                        throw new RuntimeException(e);  
                    } catch (BrokenBarrierException e) {  
                        throw new RuntimeException(e);  
                    }  
                    long before = System.currentTimeMillis();  
                    roadFirst(index);  
                    tunnel(index);  
                    roadSecond(index);  
                    synchronized (monitor) {  
                        if (winnerIndex == -1) {  
                            winnerIndex = index;  
                        }  
                    }  
                    long after = System.currentTimeMillis();  
                    score.put(index, after - before);  
                    countDownLatch.countDown();  
  
                }  
            });  
        }  
        try {  
            countDownLatch.await();  
        } catch (InterruptedException e) {  
            throw new RuntimeException(e);  
        }  
        for (int key : score.keySet()) {  
            System.out.println(key + " " + score.get(key));  
        }  
        System.out.println("Winner is " + winnerIndex + " Time: " + score.get(winnerIndex));  
    }  
  
    private static void sleepRandomTime() {  
        long millis = (long) (Math.random() * 5000 + 1000);  
        try {  
            Thread.sleep(millis);  
        } catch (InterruptedException e) {  
            throw new RuntimeException(e);  
        }  
    }  
  
    private static void prepare(int index) {  
        System.out.println(index + " started preparing");  
        sleepRandomTime();  
        System.out.println(index + " finished preparing");  
    }  
  
    private static void roadFirst(int index) {  
        System.out.println(index + " started roadFirst");  
        sleepRandomTime();  
        System.out.println(index + " finished roadFirst");  
    }  
  
    private static void roadSecond(int index) {  
        System.out.println(index + " started roadSecond");  
        sleepRandomTime();  
        System.out.println(index + " finished roadSecond");  
    }  
  
    private static void tunnel(int index) {  
        try {  
            tunnelSemaphore.acquire();  
            System.out.println(index + " started tunnel");  
            sleepRandomTime();  
            System.out.println(index + " finished tunnel");  
        } catch (InterruptedException e) {  
            throw new RuntimeException(e);  
        } finally {  
            tunnelSemaphore.release();  
        }  
    }  
}
```
### Второй способ 

```java
public class Car implements Runnable {  
    private final int carNumber;  
    private final int preparationTime;  
    private int roadTime1, tunnelTime, roadTime2;  
    private int totalTime;  
  
    private final Semaphore tunnelSemaphore;  
    private final CyclicBarrier startBarrier;  
    private final CountDownLatch finishLatch;  
    private final Random random = new Random();  
      
  
    public Car(int carNumber, int preparationTime, Semaphore tunnelSemaphore, CyclicBarrier startBarrier, CountDownLatch finishLatch) {  
        this.carNumber = carNumber;  
        this.preparationTime = preparationTime;  
        this.tunnelSemaphore = tunnelSemaphore;  
        this.startBarrier = startBarrier;  
        this.finishLatch = finishLatch;  
    }  
  
    public int getTotalTime() {  
        return totalTime;  
    }  
  
    public int getCarNumber() {  
        return carNumber;  
    }  
  
    @Override  
    public void run() {  
  
        try {  
            tunnelTime = (int) (Math.random() * 1000 + 1000);  
            roadTime2 = (int) (Math.random() * 1000 + 1000);  
  
            System.out.println("Car #" + carNumber + " is preparing for the race");  
            Thread.sleep(preparationTime);  
            System.out.println("Car #" + carNumber + " is ready for the race");  
  
            try {  
                startBarrier.await();  
            } catch (BrokenBarrierException e) {  
                throw new RuntimeException(e);  
            }  
  
            roadTime1 = random.nextInt(500) + 500;  
            System.out.println("Car #" + carNumber + " drove along the first section of the road");  
            Thread.sleep(roadTime1);  
  
            System.out.println("Car #" + carNumber + " drove up to the tunnel");  
            tunnelSemaphore.acquire();  
            System.out.println("Car #" + carNumber + " drove into the tunnel");  
            tunnelTime = random.nextInt(1000) + 1000;  
            Thread.sleep(tunnelTime);  
            System.out.println("Car #" + carNumber + " drove out of the tunnel");  
            tunnelSemaphore.release();  
  
            roadTime2 = random.nextInt(500) + 500;  
            System.out.println("Car #" + carNumber + " drove along the second section of the road");  
            Thread.sleep(roadTime2);  
  
            totalTime = preparationTime + roadTime1 + tunnelTime + roadTime2;  
            System.out.println("Car #" + carNumber + " finished the race in " + totalTime + " milliseconds");  
  
        } catch (Exception e) {  
            e.printStackTrace();  
        } finally {  
            finishLatch.countDown();  
        }  
    }  
}

public class Race {  
    private final int NUMBER_OF_CARS = 10;  
    private final int TUNNEL_CAPACITY = 3;  
  
    private Semaphore tunnelSemaphore;  
    private CyclicBarrier startBarrier;  
    private List<Car> cars;  
    public static CountDownLatch finishLatch;  
  
    public Race(Semaphore tunnelSemaphore, CyclicBarrier startBarrier, List<Car> cars, CountDownLatch finishLatch) {  
        tunnelSemaphore = new Semaphore(TUNNEL_CAPACITY, true);  
        startBarrier = new CyclicBarrier(NUMBER_OF_CARS);  
        finishLatch = new CountDownLatch(NUMBER_OF_CARS);  
        cars = new ArrayList<>();  
        prepareCars();  
    }  
  
    public Race() {  
        tunnelSemaphore = new Semaphore(TUNNEL_CAPACITY, true);  
        startBarrier = new CyclicBarrier(NUMBER_OF_CARS);  
        finishLatch = new CountDownLatch(NUMBER_OF_CARS);  
        cars = new ArrayList<>();  
        prepareCars();  
    }  
  
    public void prepareCars() {  
  
        cars = new ArrayList<>();  
        for (int i = 1; i <= NUMBER_OF_CARS; i++) {  
            cars.add(new Car(i, 1000, tunnelSemaphore, startBarrier, finishLatch));  
        }  
    }  
  
    public void startRace() {  
        for (Car car : cars) {  
            new Thread(car).start();  
        }  
    }  
  
    // Метод для определения победителя после завершения гонки  
    public Car getWinner() {  
        Car winner = null;  
        int minTime = Integer.MAX_VALUE;  
        for (Car car : cars) {  
            if (car.getTotalTime() < minTime) {  
                minTime = car.getTotalTime();  
                winner = car;  
            }  
        }  
        return winner;  
    }  
  
    public void printResults() {  
        // Метод для вывода результатов гонки.  
        System.out.println("Result race:");  
        System.out.println("----------------------------------");  
        System.out.println("| Location  | Car Number |  Time  |");  
        System.out.println("----------------------------------");  
  
        Collections.sort(cars, (car1, car2) -> car1.getTotalTime() - car2.getTotalTime());  
  
        int place = 1;  
        for (Car car : cars) {  
            System.out.printf("| %3d | %16d | %7d |\n", place, car.getCarNumber(), car.getTotalTime());  
            place++;  
        }  
  
        System.out.println("----------------------------------");  
  
        Car winner = getWinner();  
        System.out.println("Winner: Car #" + winner.getCarNumber() + " is time " + winner.getTotalTime());  
    }   
}

public class Main {  
    public static void main(String[] args) {  
        Race race = new Race();  
        race.startRace();  
  
        try {  
            race.finishLatch.await();  
            race.printResults();  
        } catch (InterruptedException e) {  
            throw new RuntimeException(e);  
        }  
    }  
}
```

