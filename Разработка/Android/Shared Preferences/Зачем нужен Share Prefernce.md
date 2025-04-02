#SharedPrefences #android #java #Bundle #Context #getter 

Он нужен, если нам нужно сохранить небольшое количество информации. Хранить парами ключ-значение.
### Используем его в проекте

Взаимодействие с ним очень похоже с методом `onSaveInstanceState()`, а точнее классом `Bundle`. 

Есть несколько реализации этого класса и они зависят от наших целей. Мы будем использовать самый быстрый и простой:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcYBFdWCz5gDdKHw9oKpo3buHXVC6kDb3FTsyhfwoAlq5c7yG8izoyfVq2jyr6QZ_37lKh1xQfgaAgj6hMBNzzPaTN8528jYJQoIaxcvajPfQmYtZk7BMpylPyDBBpzCiFThxbAtOHpV1JqfvwA9g?key=eO5eh0X0UfqJMqsKYo8tQd9h)

Инициализация происходит через метод `PreferenceManager.getDefaultSharedPreferences(Context)`. Добавление в класс происходит поэтапно:
1. `Edit()` — редактировать SharedPreferences
2. `putInt()` — положить ключ-значение
3. `Apply()` — сохранить изменение

Для того, чтобы достать, используется геттеры, только нужно указать ключ и дефолтное значение, которое ставится, если ключ не существует.

