Определение адреса в зависимости от артикула

```js
volHostV2(25696931);  // >> '//basket-02.wb.ru/vol256/part25696/25696931'

function volHostV2(nmId) {
    const nm = parseInt(nmId, 10),
          vol = ~~(nm / 1e5),
          part = ~~(nm / 1e3);
	  
    const host =
		vol >= 0 && vol <= 143 ? "//basket-01.wb.ru" 
		:vol >= 144 && vol <= 287 ? "//basket-02.wb.ru" 
		: vol >= 288 && vol <= 431 ? "//basket-03.wb.ru" 
		: vol >= 432 && vol <= 719 ? "//basket-04.wb.ru" 
		: vol >= 720 && vol <= 1007 ? "//basket-05.wb.ru"
		: vol >= 1008 && vol <= 1061 ? "//basket-06.wb.ru"
		: vol >= 1062 && vol <= 1115 ? "//basket-07.wb.ru"
		: vol >= 1116 && vol <= 1169 ? "//basket-08.wb.ru"
		: vol >= 1170 && vol <= 1313 ? "//basket-09.wb.ru"
		: vol >= 1314 && vol <= 1601 ? "//basket-10.wb.ru"
		: vol >= 1602 && vol <= 1655 ? "//basket-11.wb.ru"
		: "//basket-12.wb.ru";
		
	return `${host}/vol${vol}/part${part}/${nm}`;
}
```
