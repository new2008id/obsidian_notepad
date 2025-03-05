#android #life_cyrcle #Activity #onCreate #onDestroy #appCafe 

### Основные понятия

[[Список методов жизненных циклов]]

У `Activity` есть свой жизненный цикл. Под `Activity` следует понимать, те методы, которые вызовет система при работе с `Activity`. В какой-то момент система сама создаст Activity, присвоит значения переменным экземпляра и вызовет метод onCreate(), что `Activity` была создана.

В onCreate() устанавливается макет и можно выполнять различные действия.
```java 
setContentView(R.layout.activity_main); 
```

При перевороте устройства, система уничтожает `Activity` и перед уничтожением вызывается метод onDestroy, - это два метода жизненного цикла.

Если нужно сохранить значения определенных переменных, при пересоздании Activity, то можно переопределить метод - `onSaveInstanceState()`. В качестве параметра он принимает объект типа `Bundle`, который представляет собой коллекцию объектов, которые хранятся парами, в виде ключ-значение. 

В этот объект можно сохранять значение при помощи метод `put`.
При пересоздании Activity, обязательно нужно добавлять проверку на `null`, что `saveInstanceState` содержит сохраненные данные.

![[Pasted image 20250217162821.png]]
### Примеры использования:

```java
public class MainActivity extends AppCompatActivity {  
  
    private TextView textViewScore1;  
    private TextView textViewScore2;  
    private int score1 = 0;  
    private int score2 = 0;  
  
    @Override  
    protected void onCreate(Bundle savedInstanceState) {  
        super.onCreate(savedInstanceState);  
        EdgeToEdge.enable(this);  
        setContentView(R.layout.activity_main);  
        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {  
            Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());  
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);  
            return insets;  
        });  
  
        if (savedInstanceState != null) {  
            score1 = savedInstanceState.getInt("score1");  
            score2 = savedInstanceState.getInt("score2");  
        }  
  
        textViewScore1 = findViewById(R.id.textViewScore1);  
        textViewScore2 = findViewById(R.id.textViewScore2);  
  
        textViewScore1.setText(String.valueOf(score1));  
        textViewScore2.setText(String.valueOf(score2));  
  
        textViewScore1.setOnClickListener(view -> textViewScore1.setText(String.valueOf(++score1)));  
        textViewScore2.setOnClickListener(view -> textViewScore2.setText(String.valueOf(++score2)));  
    }  
  
    @Override  
    protected void onSaveInstanceState(@NonNull Bundle outState) {  
        super.onSaveInstanceState(outState);  
        outState.putInt("score1", score1);  
        outState.putInt("score2", score2);  
    }  
  
    @Override  
    protected void onDestroy() {  
        super.onDestroy();  
    }  
}
```


