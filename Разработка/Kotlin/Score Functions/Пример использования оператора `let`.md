#kotlin

>[! ] Код на языке `kotlin`

```kotlin
val name: String? = "Kotlin"

val length: Int? = name?.let {
    println("Name is not null: $it") // Выполнится, только если name не null
    it.length // Возвращаем длину строки
}

println("Length: $length") // Вывод: Length: 6

val nullName: String? = null
val nullLength: Int? = nullName?.let {
    it.length // Этот код не выполнится, т.к. nullName == null
}

println("Null Length: $nullLength") // Вывод: Null Length: null
```