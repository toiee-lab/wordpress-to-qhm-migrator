# QHM Migrator (QHM移行 WordPressプラグイン)

このプラグインは、QHMで作成したサイトをWordPressへ移行させることを支援します。詳しい使い方は、以下のページをご覧ください。

- [toiee Lab WordPress KB](https://wpa.toiee.jp/kb-art-cat/qhm2wp/)

## 機能概要

QHM Migrator は以下の３つの機能があります。

### 1. 準備期間のQHMへの転送機能

WordPressサイトを準備している間は、一般の訪問者には、QHMのページを表示させる機能です。サイトへのアクセスをチェックして、ログインしていなければ、 index_qhm.php に302転送を行います。

### 2. インポート機能

QHMのページ、ブログを解析し、swfu/d/ 内にある実際に使われている、リンクされている画像やファイルを移行します。また、ページは「固定ページ」、QBlogは「投稿」として、WordPressに登録します。

### 3. QHMのURLをWordPressのURLに転送

QHMのURLは、 `index.php?HogeHoge` となります。これを `/HogeHoge/` として転送します。なお、インポートされたページや投稿は、 `/Hogehoge/` スラグとして登録されているので、正しく転送されます。

## 仕様

### 仕組み

このプラグインは、 index_qhm.php にアクセスして、 `<!-- BODYCONTENTS START -->` から `<!-- BODYCONTENTS END -->` までのHTMLを取り込みます。取り込んだHTMLファイルを解析して、ブログ投稿に必要なタイトルなどを取得しています。
	
もし、QHMのテンプレートファイルを独自に改変して、上記のコメントが表示されない場合は正常に動作しません。

### 注意点

- WordPressをクリーンインストールした直後に利用することを想定しています
- ２回の取り込みなどについては、考慮していません
- 既存の投稿、カテゴリに対する配慮はありません

### できること

- 隠しページ、通常のページを全て読み込みます
- :config や SiteNavigation などのコンテンツ以外のページは読み込みません
- ブログのカテゴリを登録、反映します
- ページ、ブログに使われている画像やファイルは、取り込まれますが、それ以外は取り込みません
- 取り込む対象のファイルは、swfu/d フォルダ以下に限ります


## Change log

- [詳細は、こちら](https://github.com/toiee-lab/wordpress-to-qhm-migrator/commits/master)

### ver 0.4 (Jul 24, 2017)

**既存ページを読み込まないオプションの追加、attachを取り込む、実行時間の延長*

- 既存の投稿、ページをslug で検索をかけて、取り込まずにスキップできるようにしました
- これは、実行時間が短いサーバー、処理が遅いサーバー、ページが多すぎる場合に、数回に分けて、ページをインポートするのに役立ちます
- PHPの実行時間を180秒に延長することを試み見ます。これにより、かなり長く実行できるようになるはずです
- 今回のバージョンから、古い添付ファイル（refを使った attachフォルダのもの) も取り込めるように改良しました

### ver 0.3 (Jul 15, 2017)

**PHP5.6以上でないと動かないようにチェックをかける**

- PHP5.6以上でないと、動作できないように修正。
- 不要なコメントなどを削除
- PHPの実行環境情報を記載

### ver 0.2

**PHP5.4に対応**

- メンバ変数、メソッドの修飾子などを削除




