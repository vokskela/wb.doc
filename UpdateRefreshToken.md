- ##### Шаг 0. Для корректного обновления, нам нужно получить refresh_token.

Для этого заходим в инструменты разработчика браузера и в разделе, гдк хранятся куки (Application) удаляем куку с именем WBToken и доменом `seller.wildberries.ru`
В результате будет перевыпущено две куки с одинаковым именем WBToken и разными доменами: `passport.wildberries.ru` и `seller.wildberries.ru`.
Кука с доменом `passport.wildberries.ru` - это и есть **refresh_token**


- ##### Шаг 1. Обновление **access_token** и **refresh_token**- Шаг 1. Обновление **access_token** и **refresh_token**
Отправляете POST запрос `https://passport.wildberries.ru/api/v2/auth/grant`
В теле запроса пустой JSON вида {}
В заголовках `'Cookie' => WBToken=refresh_token`
В ответ получаем JSON:
```json
{"token":"Ae1111111..."}
```

- ##### Шаг 2.
Отправляете POST `https://seller.wildberries.ru/passport/api/v2/auth/login`
В теле запроса с JSON вида
```json
{
	"token":"Ae1111111...",
	"device":"Macintosh",
	"version":"Google Chrome 109.0"
}
```
тут токен, который получили на предыдущем шаге.
В заголовках - НИЧЕГО❗️
В ответ приходит пустой JSON вида
```json
{"cookie":{},"token":""}
```
и кука WBToken.
Сохраняем❗️❗️❗️
Это будет ваш **access_token**, который вы будете использовать для запросов

- ##### Шаг 3.
Отправляете POST запрос `https://seller.wildberries.ru/passport/api/v2/auth/grant`
В теле запроса пустой JSON вида {}
В заголовках `'Cookie' => WBToken=access_token`
В ответ получаем JSON вида
```json
{"token":"Ae2222222..."}
```
*Временный токен*, который мы обменяем на следующем шаге

- ##### Шаг 4.
Отправляете POST запрос `https://passport.wildberries.ru/api/v2/auth/login`
В теле запроса с JSON вида
```json
{
	"token":"Ae2222222...",
	"device":"Macintosh",
	"version":"Google Chrome 109.0"
}
```
тут токен, который получили на предыдущем шаге.
В заголовках `'Cookie' => WBToken=refresh_token`
Внимание ❗️❗️❗️ Тут используется тот же токен, что и в **Шаге 1**
В ответ приходит пустой JSON вида
```json
{"cookie":{},"token":""}
```
и кука WBToken.
Сохраняем❗️❗️❗️
Это будет ваш **refresh_token**  для следующего цикла обновления

Время жизни **access_token** - 10 дней
Время жизни **refresh_token** - 14 дней