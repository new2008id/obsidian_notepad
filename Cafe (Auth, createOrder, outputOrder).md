# Разработка

## Верстка

начало - LoginActivity.java

Использовать LinearLayout в XML
Картинки с маленькой буквы и спец символов

## Написание кода в activity (Экран MainActivity)

1.  Создать активность для другого экрана
2. Создать Intent
3. Для Intent нужен доступ к editText - name, password
4. Дальше получить текст введенный пользователем (getText) и убрать пробелы.
5. Сделать проверку на наличие isEmpty name and password
6. вложить в intent - name, password, через метод putExtra()
7. Сделать валидацию полей, Toast
8. В условиях добавить else if Toast.makeText()

## Написание кода в activity (Экран MainActivity)

1. добавить события на radiobutton (onClickchangedrink)
2. добавить на картинку событие (onClickSendOrder)
3. добавить и инициализировать их в конструкторе, доступ на элементы textViewHello, additions, checkbox, spinner
4. создать строку, которая будет хранить название выбранного напитка из строковых ресурсов
5. Получить данные из intent, - name, password, присвоить им значения
6. Сделать проверку на наличие name, password, через hasExtra(), иначе сделать string defaultName = клиент, defaultPassword = пароль 
7. Сделать String.format приветствия
8. Обработка onClickChangeDrink. Получить radioButton = сделать приведение типов к (RadioButton) view
9. Присвоить ID RadioButton в макете
10. Проверить на наличие id и присвоить getString(R.string.tea / coffee)
11. Инициализировать строку для форматирования строки с напитками
12. установить текст в соответствии с данной строкой.
13. Создать объект String.Builder
14. и инициализировать его.
15. В методе onClickSendOrder()
16. Если на нем были какие-то значение, потребуется очистить его Builder.setLength = 0;
17. Требуется проверить, какой статус был нажат checked 3 раза
18. После собрать все данные собрать String order. Через String.format - Имя, пароль, напиток, вид напитка, 

## Написание кода в activity (Экран OrderActivity) 

1. В макете единственный элемент TextView - выровнять по центру. match_conctraint
2. Задать размер 72sp
3. Делаем ссылку на TextView
4. Получить заказ из предыдущей активность
5. Intent getIntent();
6. Проверить содержит ли данный ключ order
7. А иначе, отправить пользователя в LoginActivity
8. Добавить элемент ScrollView
9. ЗАвисимости расположения перенести с TextView, к ScrollView