#file #inputOutput #java 
### Основные понятия

>[! ] Класс `File` представляет файл или каталог в файловой системе. 

>[!warning ] Он предоставляет методы для `работы с файлами и каталогами`, такие как создание, удаление, переименование, проверка существования, получение информации (размер, дата изменения и т.д.). `File` _не_ используется для чтения или записи данных в файл. 

>[!error ] Для этого используются `потоки`.

### Применение:

- **Основные методы:**
    - `File(String pathname)`: Создает объект `File` для заданного пути.
    - `exists()`: Проверяет, существует ли файл или каталог.
    - `isFile()`: Проверяет, является ли объект файлом.
    - `isDirectory()`: Проверяет, является ли объект каталогом.
    - `createNewFile()`: Создает новый файл. Возвращает `true`, если файл был успешно создан, и `false`, если файл уже существует.
    - `mkdir()`: Создает новый каталог.
    - `mkdirs()`: Создает новый каталог, включая все необходимые родительские каталоги.
    - `delete()`: Удаляет файл или каталог.
    - `renameTo(File dest)`: Переименовывает файл или каталог.
    - `length()`: Возвращает размер файла в байтах.
    - `lastModified()`: Возвращает время последнего изменения файла в миллисекундах с 1 января 1970 года.
    - `getName()`: Возвращает имя файла или каталога.
    - `getPath()`: Возвращает путь к файлу или каталогу.
    - `getAbsolutePath()`: Возвращает абсолютный путь к файлу или каталогу.
    - `getParent()`: Возвращает путь к родительскому каталогу.
    - `listFiles()`: Возвращает массив объектов `File`, представляющих файлы и подкаталоги в каталоге.

### Примеры использования:

```java
public class Main {  
    public static void main(String[] args) {  
        String path = "directory1/directory2/";  
        File directories = new File(path);  
        List<File> files = new ArrayList<>();  
        files.add(new File(path + "A1.txt"));  
        files.add(new File(path + "A2.txt"));  
        files.add(new File(path + "A3.txt"));  
        files.add(new File(path + "B4.txt"));  
        files.add(new File(path + "B5.txt"));  
  
        try {  
            directories.mkdirs();  
            for (File file : files) {  
                file.createNewFile();  
            }  
        } catch (Exception e) {  
            throw new RuntimeException(e);  
        }  
  
        File[] filtered = directories.listFiles((_, name) -> name.startsWith("A"));  
        assert filtered != null;  
        for (File file : filtered) {  
            System.out.println(file.getAbsolutePath());  
        }  
    }  
}
```

**Взаимодействие `File` и потоков:**

Класс `File` используется для представления файла или каталога, а потоки используются для чтения и записи данных в файл. Вы создаете объект `File`, чтобы указать, с каким файлом вы хотите работать, а затем используете этот объект для создания потока (например, `FileInputStream` более подробно он приведен в [[Чтение из файла, класс FileInputStream и try с ресурсами]] или `FileReader`).
