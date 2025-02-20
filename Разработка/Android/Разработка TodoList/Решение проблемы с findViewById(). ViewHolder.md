#findViewById #View #ViewHolder #RecyrclerView #inflate #TextView #itemView
### Основные понятия

Проблемa с `inflate()` решена, он вызывается всего лишь 10-12 раз. Но мы не решили другую проблему — `findViewById()` будет вызываться также 20.000 раз. Желательно воспользоваться с таким классом, который будет хранить ссылку на уже найденные `View-элементы`, которые не будут вызываться столько же разом. Для этого существует специальная реализация для класса: `ViewHolder` (держатель `View-элементов`).
### Пример реализации ViewHolder:

```java
class NotesViewHolder extends RecyclerView.ViewHolder {  
    private TextView textViewNote;  
    public NotesViewHolder(@NonNull View itemView) {  
        super(itemView);  
        textViewNote = itemView.findViewById(R.id.tvNote);  
    }  
}
```

>[!success ] Мы создаем вложенный класс и наследуемся от вложенного класса `ViewHolder`. 

>[!success ] В полях указываем те view-элементы, с которыми мы хотим работать, в нашем случае — это `textView`. 

>[!success ] В конструкторе переопределяется публичная переменная ссылочного типа (`View`) `itemView` в конструктор. 

>[!success ] В нем же через нее находим `View-элемент` и присваиваем для `textView`.

[[Реализация ViewHolder для остальных методов]]

