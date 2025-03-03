#json #ArrayList 
### Основные понятия

Обычно нам прилетает огромный `JSON-ответы`. Конечно, ненужно создавать классы и поля все, создаем столько, сколько нам нужно. 

Соблюдается шаги снизу вверх. Если нам нужно получить ссылку на изображение, нам нужно создать `JSON-объект` как класс, потом создать ещё (если есть) `JSON-объект` как класс и в полях указать тот класс, а если выше находится `JSON-массив`, то создать поля-массивы (`ArrayList`), в которых будет храниться нижний `JSON-объект` (класс) по иерархию.
### Применение:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcRjKksPFz1RSXKDwKgKx942dgJtHSFWbOc3g9NG3J9Cn6Upz9OGsP1wJM-QmUgwTq2WD4cuOoEkNKZALci0Gwc5pToLda3CPDuneTji6_dDru3vdtZRARh3xeOTh7OySRaOG4X19J5tse4E4g_GpE?key=AAS-TwBkK2b7U6Fr4krzgejH)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdHYtA6hNvx3xfBaTiGugrOs62wyuULfrMfeoqABgQ69dWqkAtVtaKH_vbNk_7evEUtTIJwXBLwnekMdjb_pCDiVcU6YDyWiu8hUFAqxOHfLDdL87uaLUDC3_o_DFYTYeYyu_cToy1e5lAES6XQbBI?key=AAS-TwBkK2b7U6Fr4krzgejH)

[[Создание POJO-объектов]]