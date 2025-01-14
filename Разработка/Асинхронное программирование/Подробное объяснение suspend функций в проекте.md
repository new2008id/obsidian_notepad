### Описание:

```kotlin
lifecycleScope.launch {  
    loadData()  
}
```
В данном коде происходит инициализация coroutines scope, который уже имеет жизненный цикл, для предотвращения ошибок. Запускает корутину (`Coroutine`) в области видимости жизненного цикла `Activity`(`lifecycleScope`). Это гарантирует, что `Coroutine` будет отменена, когда `Activity` будет уничтожена, предотвращая утечки памяти.

Дальнейшие функции потребуется переделать на [[suspend-функции]]

Теперь, все методы потребуется переделать с использованием ключевого слова ***suspend*** 

```kotlin
private suspend fun loadData() {  
        binding.progress.isVisible = true  
        binding.buttonLoad.isEnabled = false  
        val city = loadCity()  
        binding.tvLocation.text = city  
        val temperature = loadTemperature(city)  
        binding.tvTemperature.text = temperature.toString()  
        binding.progress.isVisible = false  
        binding.buttonLoad.isEnabled = true  
    }  
  
    private suspend fun loadCity(): String {  
        delay(5000)  
        return "Moscow"  
    }  
  
    private suspend fun loadTemperature(city: String): Int {  
            this,  
            "Loading temperature for city: $city",  
            Toast.LENGTH_SHORT  
        ).show()  
        delay(5000)  
        return 17  
    }
```

Вместо `threed{}`, теперь используется задержка - `delay()`, которая не блокируется поток. Эта функция приостанавливает `coroutines` на заданное время, не блокируя поток, и возобновляет её выполнение по истечении указанного времени. 

Эта приостанавливающая функция может быть отменена. Если `Job` текущей `coroutines` отменяется или завершается, пока эта функция ожидает, она немедленно возобновится с исключением `CancellationException`. 

Предоставляется гарантия немедленной отмены. Если `Job` был отменен, пока эта функция была приостановлена, она не возобновит выполнение успешно.