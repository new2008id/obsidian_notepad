## Данный проект был переписан на Coroutines Scope:

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
            lifecycleScope.launch {  
                loadData()  
            }  
        }         
    }  
  
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
}
```

[[Подробное объяснение suspend функций в проекте]]