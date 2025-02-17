#java #Reader #Writer #RandomAccessFile #Scanner 

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdKsmwT8smQpDeteY6ImvleB98KJLw44wjr3uzi79iOgBNihQRrs9FUJbq7sPz5wqFr9vqJZlCEWtD3xgWFDgXyk1TOeJ4u-wx2LT-o5TDMHrQVdw_n2yP0yk2gVVWuoXIRDLUGplL_OaUfawtM73U?key=vlpyEV5X9-Tt905rl3DTuRM6)**
### Основные понятия

`Reader` и `Writer` — это абстрактные базовые классы для всех символьных потоков ввода и вывода в Java. Они работают с данными как с последовательностью 16-битных символов Unicode, что делает их подходящими для работы с текстовыми данными.

- **`Reader`:**
    
    - Предназначен для чтения символьных данных.
    - Основные методы:
        - `read()`: Читает один символ или блок символов.
        - `close()`: Закрывает поток.
    - Примеры реализации:
        - `FileReader`: Читает символы из файла.
        - `BufferedReader`: Добавляет буферизацию для повышения производительности чтения символов. Также предоставляет метод `readLine()` для чтения строк.
        - `InputStreamReader`: Мост между байтовыми и символьными потоками: преобразует байты в символы, используя заданную кодировку.
- **`Writer`:**
    
    - Предназначен для записи символьных данных.
    - Основные методы:
        - `write()`: Записывает один символ или блок символов.
        - `flush()`: Принудительно сбрасывает буфер в базовый поток.
        - `close()`: Закрывает поток.
    - Примеры реализации:
        - `FileWriter`: Записывает символы в файл.
        - `BufferedWriter`: Добавляет буферизацию для повышения производительности записи символов. Предоставляет метод `newLine()` для записи символа новой строки.
        - `OutputStreamWriter`: Мост между байтовыми и символьными потоками: преобразует символы в байты, используя заданную кодировку.

- `RandomAccessFile` — это класс в Java, который позволяет читать и записывать данные в файл в произвольном порядке. В отличие от `FileInputStream` и `FileOutputStream`, которые позволяют только последовательный доступ к файлу, `RandomAccessFile` позволяет перемещаться по файлу и читать или записывать данные в любой позиции.
    
- **Режимы доступа:**
    
    - `"r"`: Только чтение. Файл должен существовать.
    - `"rw"`: Чтение и запись. Если файл не существует, он будет создан.
    - `"rws"`: Чтение и запись, синхронизированные с содержимым. Каждое изменение содержимого файла немедленно записывается на диск.
    - `"rwd"`: Чтение и запись, синхронизированные с метаданными. Каждое изменение метаданных файла немедленно записывается на диск.
- **Основные методы:**
    
    - `RandomAccessFile(File file, String mode)`: Создает объект `RandomAccessFile` для заданного файла и режима доступа.
    - `RandomAccessFile(String name, String mode)`: Создает объект `RandomAccessFile` для заданного имени файла и режима доступа.
    - `seek(long pos)`: Устанавливает указатель файла в заданную позицию (в байтах).
    - `getFilePointer()`: Возвращает текущую позицию указателя файла (в байтах).
    - `length()`: Возвращает длину файла в байтах.
    - `read()`: Читает один байт.
    - `read(byte[] b)`: Читает массив байтов.
    - `readInt()`, `readLong()`, `readFloat()`, `readDouble()`, `readUTF()`: Читает данные различных типов.
    - `write(int b)`: Записывает один байт.
    - `write(byte[] b)`: Записывает массив байтов.
    - `writeInt()`, `writeLong()`, `writeFloat()`, `writeDouble()`, `writeUTF()`: Записывает данные различных типов.
    - `close()`: Закрывает файл.
### Примеры использования:

```java
public class Main {  
    public static void main(String[] args) {  
        String nameIsDirectory = "myPath";  
        File directory = new File(nameIsDirectory);  
        File file = new File(nameIsDirectory, "names.txt");  
  
        try (RandomAccessFile randomAccessFile = new RandomAccessFile(file, "rw")) {  
            randomAccessFile.seek(5000);  
            byte[] arr = new byte[1024];  
            randomAccessFile.read(arr);  
            System.out.println(new String(arr));  
  
            randomAccessFile.seek(0);  
            randomAccessFile.read(arr);  
            System.out.println(new String(arr));  
  
  
            randomAccessFile.seek(10);  
            randomAccessFile.writeBytes("***********************************");  
  
            randomAccessFile.seek(1000);  
            randomAccessFile.writeBytes("***********************************");  
  
            randomAccessFile.seek(200);  
            randomAccessFile.writeBytes("***********************************");  
        } catch (Exception e) {  
            e.printStackTrace();  
        }  
    }  
}
```
### Примеры использования:

```java
public class DZ_3 {  
    public static void main(String[] args) {  
        String nameIsDirectory = "myDZ";  
        File directory = new File(nameIsDirectory);  
        File file = new File(nameIsDirectory, "text.txt");  
  
        try (RandomAccessFile randomAccessFile = new RandomAccessFile(file, "r")) {  
            Scanner scanner = new Scanner(System.in);  
            byte[] pageSize = new byte[300];  
            System.out.print("Enter number page: ");  
            String numberPage = scanner.nextLine();  
            randomAccessFile.seek((long) (Integer.parseInt(numberPage) - 1) * pageSize.length);  
  
            while (!numberPage.equals("stop")) {  
                randomAccessFile.read(pageSize);  
                System.out.println(new String(pageSize));  
                System.out.print("Enter number page: ");  
                numberPage = scanner.nextLine();  
            }  
        } catch (Exception e) {  
            e.printStackTrace();  
        }  
    }  
}
```

>[!success ] `Reader` и `Writer` — это базовые классы для символьных потоков.

>[!success ] Используйте `FileReader`, `FileWriter`, `BufferedReader`, `BufferedWriter`, `InputStreamReader` и `OutputStreamWriter` для работы с текстовыми данными.
 
 >[!success ] `RandomAccessFile` позволяет читать и записывать данные в файл в произвольном порядке.

>[!success ] Используйте `seek()` для перемещения по файлу.

>[!success ] `RandomAccessFile` работает с байтами, поэтому подходит для работы с двоичными данными.

>[!success ] Обязательно закрывайте потоки и файлы после завершения работы с ними.

>[!success ] Обрабатывайте исключения при работе с файлами и потоками.


