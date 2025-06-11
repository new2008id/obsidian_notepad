#kotlin

>[! ] Код на языке `kotlin`

```kotlin
data class Person(var name: String, var age: Int)

fun main() {
    val person = Person("Alice", 30)

    val description = with(person) {
        name = "Alicia" // Изменяем имя
        age + 5 // Вычисляем возраст через 5 лет (значение возвращается)
    }

    println("Person: $person, Description: $description") 
    // Person: Person(name=Alicia, age=30), Description: 35
}
```