#java #Scanner #try_resources #FileInputStream #StringBuilder #OutputStream
### Основные понятия

Класс `Scanner` в Java предоставляет удобный способ чтения данных различных типов (целых чисел, чисел с плавающей точкой, строк и т.д.) из различных источников (например, из файла, консоли, строки). Он упрощает процесс разбора входных данных и преобразования их в нужный формат.
### Применение:

- **Основные методы:**
    
    - `Scanner(InputStream source)`: Создает объект `Scanner` для чтения данных из заданного потока ввода.
    - `Scanner(File file)`: Создает объект `Scanner` для чтения данных из заданного файла.
    - `hasNext()`: Возвращает `true`, если в потоке есть еще данные для чтения.
    - `hasNextInt()`: Возвращает `true`, если следующий токен в потоке является целым числом.
    - `hasNextDouble()`: Возвращает `true`, если следующий токен в потоке является числом с плавающей точкой.
    - `hasNextLine()`: Возвращает `true`, если в потоке есть еще строка для чтения.
    - `next()`: Возвращает следующий токен в потоке как строку.
    - `nextInt()`: Читает следующий токен из потока как целое число.
    - `nextDouble()`: Читает следующий токен из потока как число с плавающей точкой.
    - `nextLine()`: Читает следующую строку из потока.
    - `useDelimiter(String pattern)`: Устанавливает разделитель для токенов. По умолчанию разделителем является пробел.
    - `close()`: Закрывает `Scanner` и освобождает ресурсы.
### Примеры использования:

```java
public class DZ_2 {  
    public static void main(String[] args) {  
        String nameIsDirectory = "myDZ";  
        File file = new File(nameIsDirectory, "input_names.txt");  
  
        try (OutputStream outputStream = new FileOutputStream(file, true)) {  
            Scanner scanner = new Scanner(System.in);  
            System.out.print("Enter your name: ");  
            String name = scanner.nextLine();  
  
            while (!name.equals("exit")) {  
                outputStream.write(name.getBytes());  
                outputStream.write("\n".getBytes());  
                System.out.print("Enter your name: ");  
                name = scanner.nextLine();  
  
            }  
        } catch (Exception e) {  
            e.printStackTrace();  
        }  
        System.out.println("All save names: ");  
        try (InputStream inputStream = new FileInputStream(file)) {  
            byte[] buffer = new byte[1024];  
            int count = inputStream.read(buffer);  
  
            StringBuilder result = new StringBuilder();  
            while (count > 0) {  
                result.append(new String(buffer, 0, count));  
                count = inputStream.read(buffer);  
            }  
            System.out.println(result.toString());  
        } catch (Exception e) {  
            e.printStackTrace();  
        }  
    }  
}
```


