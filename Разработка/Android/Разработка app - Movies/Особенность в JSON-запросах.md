#POJO #json #appMovies 
### Основные понятия

Бывает, что `JSON-ответы` требуют токены, айди и пр. параметры, дабы получить `json-ответы`. Для того, чтобы указать параметры в `json-запросе`, нужно добавить вопросительный знак, а потом указать нужный параметр.

*`https://api.kinopoisk.dev/v1.4/movie?rating.kp=7-10&sortField=votes.kp&sortType=-1&page=2&limit=5&year=2025&type=movie&token=MXTGTC1-GWVMXHR-NYNPSHM-XRJ4XCN`*

>[!warning ] Если нужно добавить ещё какие-либо параметры в `JSON-запросе`, то теперь нужно добавить символ «`&`»:

[[Обработка большого JSON-ответа]]


