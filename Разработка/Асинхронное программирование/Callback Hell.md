**Callback hell в Kotlin** — это **ситуация, когда использование обратных вызовов приводит к сложному для чтения, понимания и обслуживания коду**. Это происходит из-за глубоко вложенной структуры с множеством уровней обратных вызовов.

## Пример вложений

```kotlin
private fun load() {  
    fetchData("url1",  
        { data1 ->  
            processData(data1,  
                { processedData ->  
                    displayResult(processedData)  
                },  
                { error ->  
                    println("Error processing $error")  
                }  
            )  
        },  
        { error ->  
            println("Error fetching data: $error")  
        }  
    )  
}
```