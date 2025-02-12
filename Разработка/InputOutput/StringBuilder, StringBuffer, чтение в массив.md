#string #StringBuilder #StringBuffer #Reader #java 
### Основные понятия

`StringBuilder` и `StringBuffer` — это классы в Java, которые используются для создания и изменения строк. Они предоставляют методы для добавления, вставки, удаления и замены символов в строке.

- **Разница между `StringBuilder` и `StringBuffer`:**
    
    - **`StringBuilder`:** Непотокобезопасный (non-thread-safe). Это означает, что он не предназначен для использования в многопоточных приложениях, где несколько потоков могут одновременно изменять строку. Однако, за счет этого он работает быстрее, чем `StringBuffer`.
    - **`StringBuffer`:** Потокобезопасный (thread-safe). Это означает, что он может безопасно использоваться в многопоточных приложениях. Все его методы синхронизированы, что предотвращает гонки данных и другие проблемы, связанные с многопоточностью. Однако, синхронизация приводит к снижению производительности.

>[! ] Класс `String` иммутабельный (неизменяемый), поэтому если вам нужно формировать строку в цикле, прикрепляя к ней новые символы, то нужно использовать класс `StringBuilder`.

>[!warning ] Если нужно делать тоже самое, но из разных потоков, тогда стоит использовать класс `StringBuffer`.

>[!success ] Читать по одному байту очень долгая операция, поэтому лучше использовать чтение в `массив`.

>[!error ] Если вам нужно читать именно `символы`, а не `байты`, тогда можно использовать `Reader`, который в качестве параметра в конструктор принимает `InputStream`. Ему по желанию можно указать кодировку.
### Применение:

```java
public class Main {  
    public static void main(String[] args) {  
        String nameIsDirectory = "myPath";  
        File directory = new File(nameIsDirectory);  
        File file = new File(nameIsDirectory, "names.txt");  
        try {  
            directory.mkdir();  
            file.createNewFile();  
        } catch (IOException e) {  
            throw new RuntimeException(e);  
        }  
  
  
        try (Reader reader = new InputStreamReader(new FileInputStream(file))) {  
            long before = System.currentTimeMillis();  
            byte[] array = new byte[8];  
            int readByte = reader.read();  
  
            // Работает для одного потока  
            StringBuilder result = new StringBuilder();  
            while (readByte > 0) {  
                result.append((char) readByte);  
                readByte = reader.read(); // для чтения файла. Метод читает один байт и return int   
            }  
            System.out.println(result.toString());  
  
  
            //потокобезопасный класс StringBuffer, его методы синхронизированы и можно работать с разных потоков  
            StringBuffer result = new StringBuffer();  
            while (readFile != -1) {  
                result.append((char) readFile);  
                readFile = inputStream.read();  
            }  
            System.out.println(result.toString());  
            long after = System.currentTimeMillis();  
            System.out.println("Time: " + (after - before) + "ms.");  
        } catch (Exception e) {  
            e.printStackTrace();  
        }  
    }  
}
```

Для того чтобы читать данные в массив можно использовать `InputStream`, `Reader`, 

[[Использование InputStream и Reader]]

**Ключевые моменты:**

>[!success ] `StringBuilder` используется для создания и изменения строк в однопоточном приложении, а `StringBuffer` — в многопоточном.

>[!success ] `StringBuilder` работает быстрее, чем `StringBuffer`, но не является потокобезопасным.

>[!success ] Для чтения данных в массив используйте методы `read()` классов `InputStream` или `Reader`.

>[!success ] При чтении в массив байтов учитывайте размер файла, чтобы создать массив нужного размера.

>[!success ] После чтения данных в массив вы можете преобразовать их в строку или использовать для других целей.


