#java #android #mobile 
# Работа с жизненными циклами приложения.
![[Pasted image 20241105223053.png]]

## Переопределение методов 

В MainActivity.java переопределяются 2 метода. Инициализируется super класс onStop(). Создаётся дополнительная переменная wasRunning, которая точно будет проверять был ли запущен метод ***onStop()***.
```java
@Override  
protected void onStop() {  
    super.onStop();  
    wasRunning = isTimerRunning;  
    isTimerRunning = false;  
}
```

```java
@Override  
protected void onStart() {  
    super.onStart();  
    isTimerRunning = wasRunning;  
}
```

В метод onSaveInstanceState также добавляем новую пару, ключ и значение для сохранения состояния ***outState.putBoolean("wasRunning", wasRunning);***
```java
@Override  
protected void onSaveInstanceState(@NonNull Bundle outState) {  
    super.onSaveInstanceState(outState);  
    outState.putInt("seconds", seconds);  
    outState.putBoolean("isTimerRunning", isTimerRunning);  
    outState.getBoolean("wasRunning", wasRunning);  
}
```

В методе ***onCreate()*** проверяем, чтобы ***savedInstanceState*** был определен. И для каждой переменной состояния, в соответствии с ключами сохраняем их состояние.

```java
if (savedInstanceState != null) {  
    seconds = savedInstanceState.getInt("seconds");  
    isTimerRunning = savedInstanceState.getBoolean("isTimerRunning");  
    wasRunning = savedInstanceState.getBoolean("wasRunning");  
}  
runTimer();
```

