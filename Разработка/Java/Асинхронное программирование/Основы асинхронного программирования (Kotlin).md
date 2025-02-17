## Проект имитируемой загрузки данных, по городу

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
            loadData()  
        }  
    }  
  
  
    private fun loadData() {  
        binding.progress.isVisible = true  
        binding.buttonLoad.isEnabled = false  
        loadCity {  
            binding.tvLocation.text = it  
            loadTemperature(it) {  
                binding.tvTemperature.text = it.toString()  
                binding.progress.isVisible = false  
                binding.buttonLoad.isEnabled = true  
            }  
        }    
    }  
  
    private fun loadCity(callback: (String) -> Unit) {  
        thread {  
            Thread.sleep(5000)  
            callback.invoke("Moscow")  
        }  
    }  
  
    private fun loadTemperature(city: String, callback: (Int) -> Unit) {  
        thread {  
            Toast.makeText(  
                this,  
                "Loading temperature for this $city",  
                Toast.LENGTH_SHORT  
            ).show()  
            Thread.sleep(5000)  
            callback.invoke(17)  
        }  
    }  
}
```

[[Как всё работает. Контекст проекта]]