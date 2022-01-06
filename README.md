# マルチブラウザ対応

## 修正
| code | 言語 | 修正概要 | 概要 |
| -------- | -------- | -------- | -------- | 
|[runtimeStyle](#runtimeStyle)|JavaScript|jqueryかclass指定に置き換える|指定した要素に対してCSSのスタイルを設定|
|[ActiveXObject](#ActiveXObject)|JavaScript|ActiveXObject関連の処理を消す(フロント)|XMLHTTPオブジェクトの生成|
|[html開始タグ](#html開始タグ) | HTML |書き換える| 古いIE対応用が書かれている|
|[id指定](#id指定)|JavaScript|`$('ID').~~~`をjqueryに書き換え|上記の修正で非対応になります
|[TDC / GET,POST通信](#TDC/GET,POST通信)|HTML/JavaScript|TDCでのテーブル生成を<br>ajax&HTMLクローンに置き換え|TDCは非対応|
|[<input&nbsp;type="image">](#<input&nbsp;type="image">)|HTML/JavaScript|<input type="image">を\<img>にする|<input type="image">はsubmitしてしまうためNG|
|[GCom.fncGetJsonFromRs()](#新しくレコードセットを作る)|VBS|新しくレコードセットを作る|レコードセットをVBSで加工して出力しており、素直にJSONにできない場合|


## 追加
|   概要    |   言語   |   適用箇所 |
| -------- | -------- | -------- |
| [Jquery3\.6\.0](#Jquery3.6.0) | HTML | jquery使いたい所 |
| [YMMaskEdit.js](#YMMaskEdit\.js) | JavaScript | input[class="ym"] を使用しているPG |


## 共通処理編集
|      PG     |    概要   |
| ----------- | -------- |
| [default.css](#default.css) | 共通CSS |
| [script_high.js](#script_high.js) | 共通JavaScript |


------------------------------

## **[runtimeStyle](https://js.studio-kingdom.com/jquery/css/css)**
> [color=red]指定した要素に対してCSSのスタイルを設定

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


------------------------------

## **[ActiveXObject](http://akon.sakura.ne.jp/map/activexobject.htm)**
### <span style="color:red;">フロントでは</span>使用不可
>ActiveXとは、Microsoft社のソフトウェア技術のブランド名の一つで、インターネットなどの通信ネットワークを通じて異なるコンピュータ上で動作するソフトウェアを連携させたり、データやプログラム部品をやり取りするための技術や製品、仕様などのこと。<br>

> Internet 経由で, 遠隔マシンの操作ができる<br>
> ActiveWindow を最大化することができる<br>
> ActiveX に準拠した 4 つのスクリプト言語という言い方があるらしい<br>



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


------------------------------

## **[Jquery3\.6\.0](https://api.jquery.com/)**

追加

``` HTML
<script type='text/javascript' src="<%=Application("SCRIPT")%>jquery-3.6.0.min.js"></script>
```

**[Jqueryエラーチェッカー](https://qiita.com/eri/items/f1e2cd905573c6517f13)**
> バージョンアップに伴って削除・変更された関数などの動かなくなった部分の補完をし、コンソールに表示して教えてくれるプラグインです。どこを修正すればよいのかが分かります。

<span class="txtred">※ jquery読込みタグの後に記述してください。</span>
``` HTML
<script src="https://code.jquery.com/jquery-migrate-3.3.2.js"></script> <!-- 開発終了時削除してください -->
```

------------------------------

## **[YMMaskEdit\.js](#YMMaskEdit\.js)**
> `web/css/YMMaskEdit.js`

> [color=red] `<input type="text" class="ym">` の.htcをJSに直したもの

注意
- inputのクラス名が大文字で`YM`となっている機能がありますが、CSS的に小文字でないといけないので`ym`に修正してください。
- 一部理解不能な記述がありましたが、スルーしました。
    ``` JavaScript
    var oEvent = createEventObject();
    var Result = new Object();
    Result.name = element.id
    Result.nakami = srcText
    oEvent.dialog = Result;
    OnDateChanged.fire(oEvent);
    ```


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


------------------------------

## **[TDC/GET,POST通信](#TDC/GET,POST通信)**
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


------------------------------

## [<input type="image">](https://xiyuan.jp/html/259/)

> [color=red] .htcファイルから各処理をjquery製のイベントなどに移植する。

> 独自関数やnameなどの見落としに注意。<br>
> 通信系はajaxに変える

NG
``` HTML
<input type="image" search="on" oncodechange="fnOnCodeChange()" class="class" id="TENPO_SELECT" alt="店舗選択"  src="<%=Image(0)%>" />
```
対応
> imgタグにする
``` HTML
<!-- HTML -->
<img class="class" id="TENPO_SELECT" src="<%=Image(0)%>" alt="店舗選択" />
```
``` JavaScript
/* JavaScript */
$(document).on('click', '#TENPO_SELECT', function() {
    // クリックイベント
}
```

------------------------------

## [新しくレコードセットを作る](https://www.depthbomb.net/?p=647)

> [color=red] レコードセットをVBSで加工しており、素直にJSONにできない場合

`Response.write`で出力してい項目を、新しいレコードセットに入れていく

```
' Sample

Dim sJsonGet  ' JSON
Dim objRS     ' newレコードセット
Set objRS = CreateObject("ADODB.Recordset")

'レコードセットのフィールドを定義
objRS.Fields.Append "CODE", 200, 500  '200:VarChar(500)
objRS.Fields.Append "KANA", 200, 500  '200:VarChar(500)
objRS.Fields.Append "RYAK", 200, 500  '200:VarChar(500)
objRS.Fields.Append "NAME", 200, 500  '200:VarChar(500)

' 純正のループ
Do Until ODynaset.EOF
    objRS.AddNew
    
    ' 分岐とか
    objRS("CODE").Value = ODynaset.Fields("CODE").Value
    objRS("KANA").Value = ODynaset.Fields("KANA").Value
    objRS("RYAK").Value = ODynaset.Fields("RYAK").Value
    objRS("NAME").Value = ODynaset.Fields("NAME").Value
    
    objRS.Update
    ODynaset.MoveNext
Loop

' 新しいレコードセットをJSONに変換して出力
objRS.MoveFirst
sJsonGet = GCom.fncGetJsonFromRs(objRS, "TEN_C")
Response.Write sJsonGet

' ちゃんと閉じる
objRS.Close
Set objRS = Nothing
ODynaset.Close
Set ODynaset  = Nothing
GCom.Disconnect

```

------------------------------

<!-- ##


------------------------------ -->

<!-- ##


------------------------------ -->

<br><br><br><br>

------------------------------

## **default\.css**
> 共通CSS
#### 新規追加

1. ``` css
    /* 非表示 */
    .nodisp {
	    display: none;
    }
    ```
1. ``` css
    /* マウスカーソルをリンク用に */
    .LinkOnMouse:hover {
	    cursor: pointer;
    }
    ```


------------------------------

## **script_high\.js**
> 共通JavaScript

#### 新規追加

> [color=red] 共通JavaScriptについての話がまとまっていないため、とりあえずここに追加

1. **<span class="txtred">JSONに直すため使用しない</span>**　**（後で削除します。）**
    ``` JavaScript    
    /**
     * [概要]  : TAB区切り文字列を連想配列へ変換
     * @pram   : value (TAB区切り文字列)
     * @pram   : key   (配列)
     * @return : 連想配列
    **/
    function tabToObject(txt, arrName) {
        var arrData = [];
        var arrData2 = [];

        txt = txt.replace(/\"/g, '').replace(/\\\"/g, '').split('\r\n');

        for (let i = 0; i < txt.length; i++) {
            arrData.push(txt[i].split('\t'));
        }

        var arrData2 =[];
        for (var i = 0; i < arrData.length; i++) {
            arrData2.push({});
            for (var j = 0; j < arrName.length; j++) {
                arrData2[i][arrName[j]] = arrData[i][j];
            }
        }

        return arrData2;
    }
    ```
    ``` JavaScript
    /* 呼び出し方法 */
    var txt     = '★TAB区切り文字列★';                 // value
    var arrName = ['AAA', 'BBB', 'CCC', 'DDD', 'EEE'];  // key
    
    var res = tabToObject(txt, arrName);  // TAB区切り文字列を連想配列へ変換
    // res.shift();  // 最初の要素(列名)削除  ※列名が設定されている場合使用
    ```


------------------------------


<!-- <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>

------------------------------ -->
<!-- 
コピペ用メモ
``` JavaScript
	/**
	 * [概要]  :
	 * @pram   :
	 * @return :
	**/
```
 -->
 
<style>
    .txtred {
        color: red;
    }
    #page-top {
        position: fixed;
        right: 50px;
        bottom: 50px;
        font-size: 2rem;
        line-height: 2rem;
        background: fff;
        color: #737373;
        padding: 10px;
        border: solid 2px;
        border-radius: 50%;
        box-shadow: 0 2px 10px -6px rgba(0,0,0,.5), 0 3px 10px -4px rgba(0,0,0,.2);
        text-decoration: none;
    }
    #page-top:hover {
        background-color: #dcdcdc;
        color: black;
    }
</style>

<a href="#マルチブラウザ対応" id="page-top" style=""><i class="blogicon-chevron-up">Top</i></a>