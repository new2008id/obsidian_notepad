## Теоретические сведения

Clean Architecture - это подход для разбиения проекта на несколько составных частей, которые еще называются сущностями (Data, Presentation, Domain)

### Domain 

Domain-слой - полностью не зависит от [[Presentation]] и [[Data]], предназначен создания структуры элементов, куда нажимает пользователь. Например - Объекты, классы, здесь должны быть описаны [[UseCase]], которые дают структуру, что конкретно умеет делать элемент. Например AddUseCase, DeleteUseCase. 
#### Примеры кода:

```kotlin
data class ShopItem(  
    val name: String,  
    val count: Int,  
    val enabled: Boolean,  
    var id: Int = UNDEFINED_ID  
) {  
    companion object {  
        const val UNDEFINED_ID = -1  
    }  
}

interface ShopListRepository {  
    fun addShopItem(shopItem: ShopItem)  
    fun deleteShopItem(shopItem: ShopItem)  
    fun editShopItem(shopItem: ShopItem)  
    fun getShopItem(shopItemId: Int): ShopItem  
    fun getShopList(): LiveData<List<ShopItem>>  
  
}

class AddShopItemUseCase(private val shopListRepository: ShopListRepository) {  
    fun addShopItem(shopItem: ShopItem) {  
        shopListRepository.addShopItem(shopItem)  
    }  
}
```

### Data

Data-слой - предназначен для конкретной реализации UseCase, тесно связан с Domain слоем, но не наоборот (Всё знает о Domain слое, a Domain слой не знает о Data - нечего!)
#### Примеры кода:

```kotlin
object ShopListRepositoryImpl : ShopListRepository {  
    private val shopListLiveData = MutableLiveData<List<ShopItem>>()  
    private val shopList = mutableListOf<ShopItem>()  
    private var autoIncrementId = 0  
  
    init {  
        for (i in 0 until 10) {  
            val item = ShopItem("name $i", i, true)  
            addShopItem(item)  
        }  
    }  
  
    override fun addShopItem(shopItem: ShopItem) {  
        if (shopItem.id == ShopItem.UNDEFINED_ID) {  
            shopItem.id = autoIncrementId++  
        }  
        shopList.add(shopItem)  
        updateList()  
    }  
  
    override fun deleteShopItem(shopItem: ShopItem) {  
        shopList.remove(shopItem)  
        updateList()  
    }  
  
    override fun editShopItem(shopItem: ShopItem) {  
        val oldElement = getShopItem(shopItem.id)  
        shopList.remove(oldElement)  
        addShopItem(shopItem)  
    }  
  
    override fun getShopItem(shopItemId: Int): ShopItem {  
        return shopList.find { it.id == shopItemId }  
            ?: throw RuntimeException("Element with id $shopItemId not found")  
    }  
  
    override fun getShopList(): LiveData<List<ShopItem>> {  
        return shopListLiveData  
    }  
  
    private fun updateList() {  
        shopListLiveData.value = shopList.toList()  
    }  
  
}

```
### Presentation 

В Presentation-слой включает в себя работу с Activity, LiveData, Fragment
#### Примеры кода:

```kotlin
class MainViewModel : ViewModel() {  
    private val repository = ShopListRepositoryImpl  
  
    private val getShopListUseCase = GetShopListUseCase(repository)  
    private val deleteShopItemUseCase = DeleteShopItemUseCase(repository)  
    private val editShopItemUseCase = EditShopItemUseCase(repository)  
  
    val shopList = getShopListUseCase.getShopList()  
  
    fun deleteShopItem(shopItem: ShopItem) {  
        deleteShopItemUseCase.deleteShopItem(shopItem)  
    }  
  
    fun changeEnabledState(shopItem: ShopItem) {  
        val newItem = shopItem.copy(enabled = !shopItem.enabled)  
        editShopItemUseCase.editShopItem(newItem)  
    }  
}

class MainActivity : AppCompatActivity() {  
    private lateinit var viewModel: MainViewModel  
    private var count = 0  
  
    override fun onCreate(savedInstanceState: Bundle?) {  
        super.onCreate(savedInstanceState)  
        enableEdgeToEdge()  
        setContentView(R.layout.activity_main)  
        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main)) { v, insets ->  
            val systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars())  
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom)  
            insets  
        }  
  
        viewModel = ViewModelProvider(this).get(MainViewModel::class.java)  
        viewModel.shopList.observe(this) {  
            Log.d("MainActivityTest", it.toString())  
            if (count == 0) {  
                count++  
                val item = it[0]  
                viewModel.changeEnabledState(item)  
            }  
        }  
  
    }  
}

```

