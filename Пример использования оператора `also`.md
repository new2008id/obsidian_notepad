#kotlin

>[! ] Код на языке `kotlin`

```kotlin
val numbers = mutableListOf(1, 2, 3)

numbers.also {
    println("Before adding: $it") // Вывод: Before adding: [1, 2, 3]
}.add(4)

println("After adding: $numbers") // Вывод: After adding: [1, 2, 3, 4]
```