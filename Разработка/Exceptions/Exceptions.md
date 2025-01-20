### Основные понятия

`Исключения (Exceptions) в Java` — это механизм обработки ошибок во время выполнения программы. Они позволяют отделять обработку ошибок от основного потока выполнения кода, делая программу более надежной, устойчивой и удобной в сопровождении.

### Применение:
    
1. **Иерархия исключений:** Все классы исключений в Java наследуются от класса `Throwable`. `Throwable` имеет два основных подкласса:
    
    - `Exception`: Представляет собой большинство ошибок, которые могут быть обработаны программой. Большинство исключений, с которыми вы столкнетесь при разработке, являются экземплярами или подклассами `Exception`.
    - `Error`: Представляет собой серьезные ошибки, такие как `OutOfMemoryError` или `StackOverflowError`. Обычно эти ошибки не обрабатываются, а приводят к аварийному завершению программы.
2. **Проверяемые и непроверяемые исключения (Checked and Unchecked Exceptions):**
    
    - **Проверяемые исключения (Checked Exceptions):** Это исключения, которые `компилятор` требует обрабатывать явно. Если метод может выбросить проверяемое исключение, то он должен либо обрабатывать его с помощью блока `try-catch`, либо объявить, что он бросает исключение с помощью ключевого слова `throws`. Примерами проверяемых исключений являются `IOException`, `SQLException` и `ClassNotFoundException`.
    - **Непроверяемые исключения (Unchecked Exceptions):** Это исключения, которые не требуют явной обработки компилятором. К ним относятся `RuntimeException` и его подклассы, такие как `NullPointerException`, `IllegalArgumentException` и `ArrayIndexOutOfBoundsException`. Эти исключения обычно возникают из-за ошибок в логике программы, а не из-за внешних факторов.

### Примеры использования:

```java
public class Main {  
    public static void main(String[] args) {  
        int a = 1;  
  
        try {  
            ArrayList<Integer> numbers = new ArrayList<>();
            for (int i = 0; i < 5; i++) {  
                numbers.add(i);  
            }  
  
            for (int i = 0; i < 6; i++) {  
                System.out.println(numbers.get(i));  
            }  
  
            int b = 7 / a;  
            int c = Integer.parseInt("fjdak;fjk;");  
        } catch (IndexOutOfBoundsException error) {  
            System.out.println("IndexOutOfBoundsException...");  
        } catch (Exception e) {  
            System.out.println("Поймано исключение: " + e.getClass());  
        }  
        System.out.println("Hello");  
    }  
}
```


