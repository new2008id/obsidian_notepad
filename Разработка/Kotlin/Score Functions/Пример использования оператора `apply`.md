#kotlin

>[! ] Код на языке `kotlin`

```kotlin
data class Book(var title: String = "", var author: String = "", var year: Int = 0)

fun main() {
    val book = Book().apply {
        title = "The Lord of the Rings"
        author = "J.R.R. Tolkien"
        year = 1954
    }

    println("Book: $book") 
    // Book: Book(title=The Lord of the Rings, author=J.R.R. Tolkien, year=1954)
}
```