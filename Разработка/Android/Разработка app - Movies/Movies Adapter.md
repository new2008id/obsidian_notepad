#RecyrclerView #Context #GridLayoutManager #MovieAdapter 
### Основные понятия

#### Колонки

Если нужно, чтобы `RecyclerView` выводил колонами (пример ниже), используется класс `GridLayoutManager()`. В конструкторе требуется указать следующие параметры:
- `Context `
- Количество колон на экране
### Применение:

![[Pasted image 20250303160531.png]]

### Примеры использования:

```java
recyclerViewMovies.setLayoutManager(new GridLayoutManager(this, 2));
```

>[!success ] Для того, чтобы добавить тени, используется параметр `app:cardUseCompatPadding=""`

>[!success ] Для того, чтобы изменить радиус округления, используется параметр  `app:cardCornerRadius=""`

[[Делаем карточки круглыми и с тенями]]