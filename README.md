# **BRJ**マルチブラウザ対応

## 修正項目

|code|type|概要|
|:--|:--:|:--|
|[runtimeStyle](#runtimeStyle)|JS|指定した要素に対してCSSのスタイルを設定|

------------------------------
## **\[[runtimeStyle](https://js.studio-kingdom.com/jquery/css/css)\]**
> 指定した要素に対してCSSのスタイルを設定

非対応
``` JavaScript
$('AAA').runtimeStyle.display = 'none';
```
対応
``` JavaScript
$('AAA').css('display', 'none');
```
------------------------------








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