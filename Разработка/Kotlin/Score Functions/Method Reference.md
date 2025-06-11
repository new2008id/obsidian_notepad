#methodReference #object #instance #class #kotlin 
### Основные понятия

Method Reference — это сокращенная форма записи лямбда-выражения, которая просто вызывает существующий метод. Вместо того, чтобы писать лямбду, которая делает то же самое, ты можешь просто сослаться на этот метод.

**Синтаксис:**

В Kotlin есть несколько видов ссылок на методы:

1. **Ссылка на метод экземпляра объекта:** `object::instanceMethod`
2. **Ссылка на метод класса (статический метод):** `Class::staticMethod`
3. **Ссылка на конструктор:** `Class::new`
4. **Ссылка на метод экземпляра через ссылку на класс (для вызова метода на экземпляре, переданном как аргумент):** `Class::instanceMethod`
### Примеры использования:

```kotlin
fun main() {  
  
    loadProduct(File("products.txt").readText()).myAlso {  
        println("Filter by category CLOTHING")  
    }.filter { it.productCategory == ProductCategory.CLOTHING }.myAlso {  
        println("Filter for a price over 500")  
    }.filter { it.productPrice > 500 }.myAlso {  
        println("Filter by rating more than 4")  
    }.filter { it.productRating > 4 }.myAlso {  
        println("Increase price by 2")  
    }.map {  
        it.copy(productPrice = it.productPrice * 2)  
        "${it.id} - ${it.productName} - ${it.productPrice}"  
    }.myAlso {  
        println("Print info")  
    }.forEach(::println)  
}
```

```kotlin
data class Person(val name: String, val age: Int) {
    fun greet() {
        println("Hello, my name is $name")
    }
}

fun main() {
    val person = Person("Alice", 30)
    // Лямбда-выражение:
    val greetWithLambda = { person.greet() }
    greetWithLambda() // Выведет "Hello, my name is Alice"
    // Method Reference:
    val greetWithMethodReference = person::greet
    greetWithMethodReference() // Выведет "Hello, my name is Alice"
}
```



