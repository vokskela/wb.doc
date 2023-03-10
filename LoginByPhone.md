- ### Шаг 1.
POST: `https://seller.wildberries.ru/passport/api/v2/auth/login_by_phone`
body:
```json
{
	"phone":"+7000000000",
	"is_terms_and_conditions_accepted":true
}
```

Ответ:
 ```json
{
	"code_length": 6,
	"till_next_request": 20000,
	"token": "TOKEN"
}
```

- ### Шаг 2.
POST: `https://seller.wildberries.ru/passport/api/v2/auth/login`
body:
```json
{
	"options":
	{
		"notify_code":"SMS_CODE"
	},
	"token":"TOKEN",
	"device":"Windows,Google Chrome 110.0"
}
```
Ответ: ...