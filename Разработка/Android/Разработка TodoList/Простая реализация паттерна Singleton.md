#Singleton #Activity #instance 
### Основные понятия

Если вам нужно, чтобы класс имел только один экземпляр себя и не пересоздавался снова (так как пересозданный класс удалит предыдущие данные из старого экземпляра (чистый новый экземпляр), либо будут создаваться новые экземпляры, которые будут никак друг друга не связаны. 
### Пример проблемы:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeQ1CYzrKqWJVJSnvvZObhVkhkF2kO4ClNDHhRm-nifz9NLDquRiEumXaZbXpnoAWGM6QQd6keenqIpB6x3F6ep34A9KZk5ST3EGXF_Y2gsvKH0FuRVbpPxHdOwOnVL4HvrFVB3oRHW9cJ0n0F4Hl4?key=wcXsxN3ue-kJC6FslyjMh8Nk)

Для этого используется паттерн проектирования Singleton. Он делает так, чтобы класс имел всего лишь один экземпляр и другие классы не могли пересоздавать или создавать новые. 
### Применение:

```java
public class Database {  
    private final ArrayList<Note> notes = new ArrayList<>();  
    private static Database instance = null;  
    public static Database getInstance() {  
        if (instance == null) {  
            instance = new Database();  
        }  
        return instance;  
    }  
  
    private Database() {  
        Random random = new Random();  
        for (int i = 0; i < 5; i++) {  
            Note note = new Note(i, "Note " + i, random.nextInt(3));  
            notes.add(note);  
        }  
    }
}
```

>[!warning ] Мы создаем статическое поле ссылочных данных `Database`, потом создаем `статический метод` и проверяем: существует экземпляр класса `Database` или нет, если да — не создается и возвращается уже созданный экземпляр класса,  если нет, то создаем новый экземпляр класса и возвращаем его.
### Примеры работы:

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd_ARRSXRIggTMGPjNOJI79_d7GbuVN1d3P7GWWcn0KVm9eg4deDO7RrdMMmFmF-2pfoiZG8GE_UzO_dkUIeoqPC5eVvRBXAzvEY7PXlriPPXQjKF2Ww1bCRf4FoB7Mdnw5mtQpQlf7NxKYCq2ma-E?key=wcXsxN3ue-kJC6FslyjMh8Nk)**

[[Решение проблемы с findViewById(). ViewHolder]]