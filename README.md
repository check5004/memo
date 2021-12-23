# マルチブラウザ対応

## **修正項目**

|code|type|発見PG|概要|
|:--|:--:|:--|:--|
|[runtimeStyle](#runtimeStyle)|JS|BJIE010.html (アイスクリーム発注入力)|指定した要素に対してCSSのスタイルを設定|
|[ActiveXObject]()|JS|transfer.js (XMLHTTPオブジェクトの生成)||

------------------------------
## **[runtimeStyle](https://js.studio-kingdom.com/jquery/css/css)**
> 指定した要素に対してCSSのスタイルを設定

### **[display](https://developer.mozilla.org/ja/docs/Web/CSS/display#display_none)**
非対応
``` JavaScript
$('AAA').runtimeStyle.display = 'none';
```
対応
``` JavaScript
/* JavaScript */
// ①
$('AAA').css('display', 'none');
$('AAA').css('display', '');
// ②
$('AAA').addClass('nodisp');
$('AAA').removeClass('nodisp');
```
``` css
/* css */
/* ② */
.nodisp {
  display: none;
}
```

### **[visibility](https://developer.mozilla.org/ja/docs/Web/CSS/visibility)**
非対応
``` JavaScript
$('AAA').runtimeStyle.visibility = 'visible';
$('AAA').runtimeStyle.visibility = 'hidden';
```
対応
```
displayと同様
```
その他marginなど

------------------------------








> コピペ
``` JavaScript
	/**
	 * [概要]  :
	 * @pram   :
	 * @return :
	**/
```

[return to top](#修正項目)