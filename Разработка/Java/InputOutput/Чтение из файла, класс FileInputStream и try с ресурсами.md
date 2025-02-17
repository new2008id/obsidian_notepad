#InputStream #file #Closable #FileInputStream #read #try_resources #java 
### Основные понятия

>[! ] Данные из файла или из сети, нужно читать по `байтам`, т. е. данные нужно превращать в поток байтов (картинку, видео или файл).

>[!warning ] Затем нужно прочитать данные байты и сделать определенные действия.

>[!success ] Для преобразования потока байтов используется `InputStream` - абстрактный класс, позволяет преобразовывать данные в поток байтов.

>[!success ] Если нужно считать данные из файла, поэтому потребуется использовать `FileInputStream` - наследник `InputStream`, позволяет преобразовать файл в поток байтов

Для побайтового чтения данных используется абстрактный класс `InputStream`

Метод `read()` возвращает значение прочитанного байта в пределах от 0 до 255 или -1, если данных в потоке больше нет.

Для чтения данных из файла используется наследник InputStream - FileInputStream.

>[!warning ] `Try с ресурсами` автоматически освобождает ресурсы по завершении операции, для этого передаваемый объект должен реализовывать интерфейс `Closable`
### Примеры использования:

```java
public class Main {  
    public static void main(String[] args) {  
        File file = new File("1.txt");  
        try {  
            file.createNewFile();  
        } catch (IOException e) {  
            throw new RuntimeException(e);  
        }  
        try (InputStream inputStream = new FileInputStream(file)) {  
  
            int a = inputStream.read(); // для чтения файла. Метод читает один байт и return int  
            while (a != -1) {  
                System.out.print((char) a);  
                a = inputStream.read();  
            }  
  
        } catch (Exception e) {  
            throw new RuntimeException(e);  
        }  
    }  
}
```
### Еще примеры:

```java
public class Main {  
    public static void main(String[] args) {  
        String nameIsDirectory = "myPath";  
        File directory = new File(nameIsDirectory);  
        
        // как один из способов создания файлов
        File file = new File(nameIsDirectory, "names.txt");  
        try {  
            directory.mkdir();  
            file.createNewFile();  
        } catch (IOException e) {  
            throw new RuntimeException(e);  
        }  
  
        try (InputStream inputStream = new FileInputStream(file)) {  
            int readFile = inputStream.read();  
            while (readFile != -1) {  
                System.out.print((char) readFile);  
                readFile = inputStream.read();  
            }  
        } catch (Exception e) {  
           e.printStackTrace();  
        }   
    }  
}
```
