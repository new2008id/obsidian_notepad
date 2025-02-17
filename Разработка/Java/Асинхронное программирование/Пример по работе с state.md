```kotlin
class MainActivity : AppCompatActivity() {  
    private val binding by lazy {  
        ActivityMainBinding.inflate(layoutInflater)  
    }  
    
    override fun onCreate(savedInstanceState: Bundle?) {  
        super.onCreate(savedInstanceState)  
        enableEdgeToEdge()  
        setContentView(R.layout.activity_main)  
        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main)) { v, insets ->  
            val systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars())  
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom)  
            insets  
        }  
        setContentView(binding.root)  
        binding.buttonLoad.setOnClickListener {   
            loadWithoutCoroutine()  
        }  
    }  
  
    private suspend fun loadData() {  
        Log.d("MainActivity", "Load started: $this")  
        binding.progress.isVisible = true  
        binding.buttonLoad.isEnabled = false  
        val city = loadCity()  
  
        binding.tvLocation.text = city  
        val temperature = loadTemperature(city)  
  
        binding.tvTemperature.text = temperature.toString()  
        binding.progress.isVisible = false  
        binding.buttonLoad.isEnabled = true  
        Log.d("MainActivity", "Load finished: $this")  
    }  
  
    private fun loadWithoutCoroutine(step: Int = 0, obj: Any? = null) {  
        when (step) {  
            0 -> {  
                Log.d("MainActivity", "Load started: $this")  
                binding.progress.isVisible = true  
                binding.buttonLoad.isEnabled = false  
                loadCityWithoutCoroutine {  
                    loadWithoutCoroutine(1, it)  
                }  
            }  
  
            1 -> {  
                val city = obj as String  
                binding.tvLocation.text = city  
                loadTemperatureWithoutCoroutine(city) {  
                    loadWithoutCoroutine(2, it)  
                }  
            }  
  
            2 -> {  
                val temperature = obj as Int  
                binding.tvTemperature.text = temperature.toString()  
                binding.progress.isVisible = false  
                binding.buttonLoad.isEnabled = true  
                Log.d("MainActivity", "Load finished: $this")  
            }  
        }  
    }  
  
    private fun loadCityWithoutCoroutine(callback: (String) -> Unit) {  
        Handler(Looper.getMainLooper()).postDelayed({  
            callback.invoke("Moscow")  
        }, 5000)  
    }  
    
    private fun loadTemperatureWithoutCoroutine(city: String, callback: (Int) -> Unit) {  
        Toast.makeText(  
            this,  
            "Loading temperature for city: $city",  
            Toast.LENGTH_SHORT  
        ).show()  
  
        Handler(Looper.getMainLooper()).postDelayed({  
            callback.invoke(17)  
        }, 5000)  
    }  
  
    private suspend fun loadTemperature(city: String): Int {  
        // если нужен Looper другого потока, то использовать Looper.myLooper() это нуллабельный объект, который нужно будет обработать  
        // если нужен Looper главного потока, то использовать getMainLooper()        Toast.makeText(  
            this,  
            "Loading temperature for city: $city",  
            Toast.LENGTH_SHORT  
        ).show()  
        delay(5000)  
        return 17  
    }  
}
```

#### Описание 

>[! ] В данном примере описано, как метод `loadWithoutCoroutine()` используются многократно, передавая разные шаги (`step`) и выдавая различный результат, по такому принципу устроены `callback` в `Coroutines`