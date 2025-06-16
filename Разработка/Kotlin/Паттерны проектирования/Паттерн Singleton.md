#Singleton #object #constructor #companionObject
### Основные понятия

Singleton - паттерн проектирования, гарантирующий, что у класса будет только один экземпляр. Используется, когда во всей программе нужен только один экземпляр какого-либо класса. 

Самая простая реализация паттерна - смена ключевого слова class на object

```kotlin
object UserRepository {  
  
    init {  
        println("Creating repository...")  
    }  
  
    private val file = File("users.json")  
    private val _users: MutableList<User> = loadAllUsers()  
    val users  
        get() = _users.toList()  
  
    private fun loadAllUsers(): MutableList<User> {  
        if (!file.exists()) file.createNewFile()  
  
        val content = file.readText().trim()  
        return Json.decodeFromString(content)  
    }
```

>[! warning ] Данный способ хорошо, подходит, когда в конструктор ничего не нужно передавать в качестве параметра.
##### Более правильная реализация:

```kotlin
class UserRepository private constructor() {  
  
    init {  
        println("Creating repository...")  
    }  
  
    private val file = File("users.json")  
    private val _users: MutableList<User> = loadAllUsers()  
    val users  
        get() = _users.toList()  
  
    private fun loadAllUsers(): MutableList<User> {  
        if (!file.exists()) file.createNewFile()  
  
        val content = file.readText().trim()  
        return Json.decodeFromString(content)  
    }  
  
    companion object {  
        private var instance: UserRepository? = null  
  
        fun getInstance(password: String): UserRepository {  
            val correctPassword = File("password.txt").readText().trim()  
            if (correctPassword != password) throw IllegalArgumentException("Incorrect password")  
            if (instance == null) {  
                instance = UserRepository()  
            }  
            return instance!!  
        }  
    }  
}
```

Данная реализация заключается в том, чтобы снаружи запретить создание экземпляра класса и для этого делается `private constructor()`. Далее создаётся метод getInstance() который возвращает экземпляр класса. И чтобы этот метод можно было вызвать, без создания других объектов, нужно поместить внутрь `companion object {}`

>[!error ] Всё, что объявлено внутри `companion object` относится к `классу`, а не к `объекту`

