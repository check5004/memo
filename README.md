# マルチブラウザ対応

## 修正項目

| code | 言語 | 修正概要 | 概要 |
| -------- | -------- | -------- | -------- | 
|[runtimeStyle](#runtimeStyle)|JavaScript|jqueryかclass指定に置き換える|指定した要素に対してCSSのスタイルを設定|
|[ActiveXObject](#ActiveXObject)|JavaScript|ActiveXObject関連の処理を消す(フロント)|XMLHTTPオブジェクトの生成|
|[html開始タグ](#html開始タグ) | HTML |書き換える| 古いIE対応用が書かれている|
|[id指定](#id指定)|JavaScript|`$('ID').~~~`をjqueryに書き換え|上記の修正で非対応になります
|[TDC&nbsp;\/&nbsp;GET\,POST通信](#TDC&nbsp;\/&nbsp;GET,POST通信)|HTML/JavaScript|TDCでのテーブル生成を<br>ajax&HTMLクローンに置き換え|TDCは非対応|


## 追加項目
|   概要    |   言語   |   適用箇所 |
| -------- | -------- | -------- |
| [Jquery3\.6\.0](#Jquery3.6.0) | HTML | jquery使いたい所 |


------------------------------

## **[runtimeStyle](https://js.studio-kingdom.com/jquery/css/css)**
> 指定した要素に対してCSSのスタイルを設定

(例)`display: none;`<br>
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

その他 margin, visibility など

<br>[return to top](#修正項目)

------------------------------

## **[ActiveXObject](http://akon.sakura.ne.jp/map/activexobject.htm)**
### "フロントでは"使用不可
>ActiveXとは、Microsoft社のソフトウェア技術のブランド名の一つで、インターネットなどの通信ネットワークを通じて異なるコンピュータ上で動作するソフトウェアを連携させたり、データやプログラム部品をやり取りするための技術や製品、仕様などのこと。<br>

> Internet 経由で, 遠隔マシンの操作ができる<br>
> ActiveWindow を最大化することができる<br>
> ActiveX に準拠した 4 つのスクリプト言語という言い方があるらしい<br>


<br>[return to top](#修正項目)

------------------------------

## **[html開始タグ](http://www.htmq.com/html5/doctype.shtml)**

削除

``` html
<?xml version="1.0" encoding="Shift_JIS"?>
<html xml:lang="ja" lang="ja" xmlns="http://www.w3.org/1999/xhtml">
```

追加
``` html
<!DOCTYPE html>
<html lang="jp">
```

<br>[return to top](#修正項目)

------------------------------

## **[Jquery3\.6\.0](https://api.jquery.com/)**

追加

``` HTML
<script type='text/javascript' src="<%=Application("SCRIPT")%>jquery-3.6.0.min.js"></script>
```

**[Jqueryエラーチェッカー](https://qiita.com/eri/items/f1e2cd905573c6517f13)**
> バージョンアップに伴って削除・変更された関数などの動かなくなった部分の補完をし、コンソールに表示して教えてくれるプラグインです。どこを修正すればよいのかが分かります。

<span style="color: red;">※ jquery読込みタグの後に記述してください。</span>
``` HTML
<script src="https://code.jquery.com/jquery-migrate-3.3.2.js"></script> <!-- 開発終了時削除してください -->
```

<br>[return to top](#修正項目)

------------------------------

## **[id指定](https://api.jquery.com/id-selector/#id1)**

非対応
``` JavaScript
$('ID').~~~~~;
```

対応
``` JavaScript
$('#ID').~~~~~;  // jquery
```

<br>[return to top](#修正項目)

------------------------------

## **[TDC&nbsp;\/&nbsp;GET\,POST通信](#TDC&nbsp;\/&nbsp;GET\,POST通信)**
TDCを使用し作成していたテーブルは、**ajax**でデータを**JSON**形式で取得し、**HTML**で作成したテーブルにセットしていくよう修正します。<br>
テーブルへのデータ追加はクローン方式が望ましいです。

**ajax**<br>
フロント
``` JavaScript
/* JavaScript */
$.ajax({
    url: url,
    type:'GET',  // or POST
    cache: false,
    async: false,
    contentType:'text/html; charset=shift_jis',
    data: data,
    error:function(e) {
        // 結果:エラー時
        alert(e);
        return;
    },
    success: function(txt, status, xhr) {
        // 結果:成功時
        // ここでテーブル作成など
    }
});
```
サーバー
``` VB
/* VB */
'レコードセット→JSON形式に変換する処理'  
sJsonGet = GCom.fncGetJsonFromRs(ODynaset, "AAAAA")
Response.Write sJsonGet
```

<br>[return to top](#修正項目)

------------------------------

##

<br>[return to top](#修正項目)

------------------------------

## 

<br>[return to top](#修正項目)

------------------------------

##

<br>[return to top](#修正項目)

------------------------------

##

<br>[return to top](#修正項目)

------------------------------


<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>

------------------------------

コピペ用メモ
``` JavaScript
	/**
	 * [概要]  :
	 * @pram   :
	 * @return :
	**/
```

<br>[return to top](#修正項目)