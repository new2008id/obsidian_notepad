#InputStream #StringBuilder #Reader #inputOutput #FileInputStream #java 
### Основные понятия

Чтение данных в массив — это распространенный способ работы с данными, полученными из потока ввода.
### Применение:

```java
public class DZ_1 {  
    public static void main(String[] args) {  
        String nameIsDirectory = "myDZ";  
        File directory = new File(nameIsDirectory);  
        File file = new File(nameIsDirectory, "names.txt");  
        try {  
            directory.mkdir();  
            file.createNewFile();  
        } catch (IOException e) {  
            throw new RuntimeException(e);  
        }  
  
        try (Reader reader = new InputStreamReader(new FileInputStream(file))) {  
	        //1. Создайте массив байтов нужного размера
            char[] arr = new char[128];  
            //2. Прочитайте данные из потока в массив
            int countSymbolsReaded = reader.read(arr);  
  
            StringBuilder result = new StringBuilder();  
            //3. Обработайте данные из массива
            while (countSymbolsReaded > 0) {  
	            // Добавляем прочитанные символы в StringBuilder
                result.append(new String(arr, 0, countSymbolsReaded));  
                countSymbolsReaded = reader.read(arr);  
            }  
            String[] names = result.toString().split(" ");  
            Arrays.stream(names)  
                    .filter(name -> name.startsWith("A"))  
                    .forEach(System.out::println);  
        } catch (Exception e) {  
            e.printStackTrace();  
        }  
    }  
}
```


