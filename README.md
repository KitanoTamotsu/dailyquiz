ワークフロー
<img width="600" src="https://user-images.githubusercontent.com/40127279/155270515-f47ca8b1-00d8-4dbc-ab5f-a86f7c28be6c.png">

#### 開発メモ
### 1.ワークフローの構成
　ScriptFilterの2段構えです
<br>　今日のクイズというサイトを見つけました
<br>　1日3題で、1題につき1ページです
<br>　さらに過去問一覧のページがあったので
<br>　1段目のScriptFilterで過去問から日付を選んで
<br>　2段目のScriptFilterで3問の出題をするようにしました
### 2.1段目のScriptFilter
　URLの解釈で、タイトルとURLをAタグから同時に抽出しています
<br>　Aタグのリンク先と表示文字列がそれぞれAlfred出力のargとtitleになります
<br>　意味はないですがsedで順番を入れ替えてitem配列に格納しています
<img width="600" src="https://user-images.githubusercontent.com/40127279/155270593-7ff7f23d-e50e-4733-880c-157c1b441efe.png">
<br>　
<br>　具体的には
<br>　item[1] 1項目目のタイトル　item[2] 1項目目のリンク先　
<br>　item[3] 2項目目のタイトル　item[4] 2項目目のリンク先
<br>　item[5] 3項目目のタイトル　item[6] 3項目目のリンク先
<br>　・・・・という配列になりますが、上記の1行を1つのAタグからセットしています
<br>　
<br>　具体的には
<br>　`<A href="リンク先URL">表示テキスト</a>`
<br>　というAタグから
<br>　表示テキスト　＋　ブランク　＋　リンク先URL　＋　ブランク　
<br>　という文字列を作り出しています
<br>　
<br>　これをgrepでAタグの数だけ取ってきてカッコで括ってitem変数に配列として格納します
<br>　
<br>　JSONフォーマットには、9つ分セットします
<br>　配列の要素数を2で割って項目数をもとめ、shuf(シャッフル)でランダムに9個抽出
<br>　sortは表示テキストの先頭が日付なので、見やすいようにソートしています
<br>　あとはJSONフォーマットへのセットでOK
### 3.2段目のScriptFilter
<br>　1日の出題が3題でそれぞれURLが違います
<br>　そのためURLをそれぞれセットして、解釈して出題文を抽出します
<br>　改行だかなんだかわからないコードが入っていたのでちょっと強引な抽出となっています
<img width="600" src="https://user-images.githubusercontent.com/40127279/155270642-7c98e749-c5d8-4499-bc1d-6c708214c3b5.png">
<br>　
<br>　JSONフォーマットでは、出題文をsubtitleにセットしています
<br>　その理由は、文字数がtitleより多くなるためです。文字が小さくなりますが。。。　
<br>　3つだけかつ別ページからの取得なので、ヒアドキュで書いています
<br>　最後はOpenURLです
<br>　
<img width="600" src="https://user-images.githubusercontent.com/40127279/155270696-e923c19d-3b77-42f5-a552-9dc40016c5d2.png">

#### 背景
　今日のクイズというサイトを見つけました
<br>　基本4択ですが、引っ掛けというか、思い違いを突いた問題があり面白いクイズです
<br>　過去問一覧に900問ほどあったので、お得意（？）のランダム表示にしました

#### 取扱説明
### 機能:
　グーグルサジェストをAlfred出力フォーマットで表示する
### インストール:
　1.[alfredworkflow](https://github.com/KitanoTamotsu/dailyquiz/releases/download/ver1.0/dailyquiz.alfredworkflow.zip)をダウンロード 
<br>　2.ファイルをダブルクリックしてワークフローに登録

### 使い方:
　Alfredからキーワード『qqq』で起動。表示されるその日のクイズを選択する
<br>
<br>
[トップページに戻る](https://kitanotamotsu.github.io/)
