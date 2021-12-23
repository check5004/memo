# マルチブラウザ対応

## **修正項目**

|code|言語|発見|概要|
|:--|:--:|:--|:--|
|[runtimeStyle](#runtimeStyle)|JavaScript|BJIE010.html|指定した要素に対してCSSのスタイルを設定|
|[ActiveXObject](#ActiveXObject)|JavaScript|transfer.js|XMLHTTPオブジェクトの生成|

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
// <1>
$('AAA').css('display', 'none');
$('AAA').css('display', '');
// <2>
$('AAA').addClass('nodisp');
$('AAA').removeClass('nodisp');
```
``` css
/* css */
/* <2> */
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

<br>[return to top](#修正項目)

------------------------------

## **[ActiveXObject](http://akon.sakura.ne.jp/map/activexobject.htm)**
>ActiveXとは、Microsoft社のソフトウェア技術のブランド名の一つで、インターネットなどの通信ネットワークを通じて異なるコンピュータ上で動作するソフトウェアを連携させたり、データやプログラム部品をやり取りするための技術や製品、仕様などのこと。<br>

> Internet 経由で, 遠隔マシンの操作ができる<br>
> ActiveWindow を最大化することができる<br>
> ActiveX に準拠した 4 つのスクリプト言語という言い方があるらしい<br>

### **[setRequestHeader](https://developer.mozilla.org/ja/docs/Web/API/XMLHttpRequest/setRequestHeader)**
>  HTTP リクエストヘッダーの値を設定

### **[getResponseHeader](https://developer.mozilla.org/ja/docs/Web/API/XMLHttpRequest/getResponseHeader)**
>  特定のヘッダー値のテキストを含んだ文字列を返します。<br>同じ名前で複数のレスポンスヘッダーがあった場合、値はコンマと空白で区切って値を接続した単一の文字列として返されます。

<br>[return to top](#修正項目)

------------------------------

<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>


------------------------------

コピペ
``` JavaScript
	/**
	 * [概要]  :
	 * @pram   :
	 * @return :
	**/
```

<br>[return to top](#修正項目)