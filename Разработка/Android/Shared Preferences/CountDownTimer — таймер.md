#CountDownTimer #TextView #onTick #onFinish #start

Когда нам нужен отсчет, таймер и пр. подобные инструменты, используется класс — CountDownTimer (Таймер обратного отсчета).

Данный класс является абстрактным и нужно переопределить методы. Достаточно использовать анонимный класс.

Переопределяться следующие методы:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf0xsLMFBMNz4-3xOwUuLDcsMzAiDFKREhyqrPgkf-Rnjcgq_58BE9HKZvIE8o7xcZwHeQqzxaQYwWKXzD39L1D_lu0lvOvzI_Gxyhu1pDyUV-HC_Fe-tnh3ZZIt71v2VtiewEEnFHl9okkAc808UA?key=eO5eh0X0UfqJMqsKYo8tQd9h)

>[! success] `onTick()` — совершает действии в теле метода во время тика
  
>[! success] `onFinish()` — совершает действия после завершения
  

Также в конструкторе нужно указать две параметры (принимает миллисекунды):

>[! warning] `millisInFuture` — с какого числа начать отсчёт
  
>[! warning] c`ountDownInterval` — сколько должно отнимать числа в `millisInFuture` в секунду.

После этого мы вызываем метод `start()`.

Также стоит сделать замечание, что таймер считает 0 также секундой. Для того, чтобы решить проблему нужно добавить ещё секунду в `onTick()` и в `onFinish()` установить в, в нашем случае в `TextView`, тексте 0.
