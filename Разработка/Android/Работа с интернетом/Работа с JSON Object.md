#JSONObject #json 
### Основные понятия

#### Преобразование JSON-ответ в конкретные объекты

В Java существует класс `JSONObject`, который может хранить `JSON-ответ` и с ним что-то делать. Для того, чтобы использовать его, нужно создать его экземпляр и в конструкторе указать `JSON-ответ`. 

Для получения ссылок и пр. информацией, нужно получать по ключевым словам в `JSON-ответе`. В нашем случае нужно получить «`message`» и «`status`». Для получения данные из `JSON-ответа` используются методы из класса `JSONObject`. В нашем случае достаточно использовать класс `getString()`, в нём мы указываем ключевые слова, из которого будет получен `объект/ссылку`.
### Примеры использования:

*MainActivity.java*
```java
private void loadDogImage() {  
    new Thread(new Runnable() {  
        @Override  
        public void run() {  
            try {  
                URL url = new URL(BASE_URL);  
                HttpURLConnection urlConnection = (HttpURLConnection) url.openConnection();  
                InputStream inputStream = urlConnection.getInputStream();  
                InputStreamReader inputStreamReader = new InputStreamReader(inputStream);  
                BufferedReader bufferedReader = new BufferedReader(inputStreamReader);  
  
                StringBuilder data = new StringBuilder();  
                String result;  
                do {  
                    result = bufferedReader.readLine();  
                    if (result != null) {  
                        data.append(result);  
                    }  
                } while (result != null);  
  
                JSONObject jsonObject = new JSONObject(data.toString());  
                String message = jsonObject.getString("message");  
                String status = jsonObject.getString("status");  
                DogImage dogImage = new DogImage(message, status);  
  
                Log.d("MainActivity", "Dog image " + dogImage.toString());  
            } catch (Exception e) {  
                Log.d("MainActivity", e.toString());  
            }  
  
        }  
    }).start();  
}
```


