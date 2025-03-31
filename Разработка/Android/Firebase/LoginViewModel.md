#Firebase #ViewModel #AndroidViewModel 

### Заметка по поводу `AndroidViewModel` и `ViewModel`

Различие у `AndroidViewModel` и `ViewModel` заключается в том, что, если нам нужен контекст, то нужно использовать суперкласс `AndroidViewModel`. Контекст требует база данных. Но если мы не нуждаемся контексту, то мы можем спокойно у наследоваться от суперкласса `ViewModel`.


