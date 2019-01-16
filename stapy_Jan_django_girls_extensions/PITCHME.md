# Next Stage of "Django Girls" Blog
### Django Girls 追加チュートリアルの紹介
#### みんなのPython勉強会#41 (2019/01/16) nikkie

---

### LT: Next Stage of "Django Girls" Blog

- [Django Girls Tutorial Extensions](https://tutorial-extensions.djangogirls.org/en/)の翻訳に参加しました
- 翻訳と動作検証で知ったことを共有します

+++

### About nikkie

- Alias @ftnext: [Twitter](https://twitter.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- 2018/09〜 stapy 4代目LT王子
- 2019/01 [エラーは友達 Django基礎ハンズオン](https://elv.connpass.com/event/114810/)
- 2019/01 [Kaggle タイタニック ハンズオン](https://supporterzcolab.com/event/677/)

+++

### LT: Next Stage of "Django Girls" Blog

1. Django Girls Tutorial Extensionsとは
2. 知ったことの共有
3. まとめ

---

### LT: Next Stage of "Django Girls" Blog

1. @color[#ff9400](Django Girls Tutorial Extensionsとは)
2. 知ったことの共有
3. まとめ

+++

### Django Girls Tutorial Extensions

- Django：PythonでWebアプリを作るためのパッケージ
- [Django Girls Tutorial](https://tutorial.djangogirls.org/ja/)：ブログアプリチュートリアル（プログラミング未経験者向け）
- Extensions：ブログアプリに機能追加する

+++

### Extensions 翻訳

- kaizumakiさん主導
- PyConJP2018 Sprintにてご協力いただく🙇
  - TakaakiFuruse
  - Jiangbinqi

+++

# Demo

---

### LT: Next Stage of "Django Girls" Blog

1. Django Girls Tutorial Extensionsとは
2. @color[#ff9400](知ったことの共有)
3. まとめ

+++

### 機能追加

- ドラフト（下書き）機能
- 投稿の削除機能
- Postモデルの`publish`メソッドという壮大な伏線を回収！
- 書きました：[Django Girls Tutorial ExtensionsをDjango2系で動かす(Part 1/3) #モグモグDjango](http://nikkie-ftnext.hatenablog.com/entry/2018/11/24/225615)

+++

### ログイン

- セキュリティ上の懸念を解消
- Django2.1から書けなくなる: `django.contrib.auth.views.login`
- Django2.1以降も使える: `django.contrib.auth.views.LoginView.as_view()`
- 原文にPR送りました💪

+++

### コメントモデル

- コメント作成機能
- コメントの承認、削除機能
- 機能追加の総決算
- 書きました：[Django Girls Tutorial ExtensionsをDjango2系で動かす(Part 3/3) コメント機能 <前編>](http://nikkie-ftnext.hatenablog.com/entry/2018/12/30/135438)

+++

### ドメイン

- dot.tkでドメインを無料で取得できる
- PythonAnywhereに設定（Webタブから静的ファイルを設定）

+++

### PostgreSQL

- PCへ導入
- Djangoに設定 (settings.py)

+++

### heroku

- kaizumakiさんのリサーチによりアップデート

---

### LT: Next Stage of "Django Girls" Blog

1. Django Girls Tutorial Extensionsとは
2. 知ったことの共有
3. @color[#ff9400](まとめ)

+++

### まとめ

- 翻訳はGitHubで確認できます：[DjangoGirlsJapan/tutorial-extensions](https://github.com/DjangoGirlsJapan/tutorial-extensions)
- Extensionsにも取り組んでみてください！（訳へのご意見お待ちしています）
- @color[#ff9400](ログイン)の実装は簡単、かつ、必要なセキュリティ対策なので、ぜひ

+++

### 今後

- 日本語版の公開に向けて動く
  - 原文の新しいソースコードの取り込み
  - 原文の修正（HerokuデプロイのWhitenoiseなど）

+++

### ご清聴ありがとうございました。
## @color[#ff9400](Happy Django Life!)
Contact: [Twitter @ftnext](https://twitter.com/ftnext)
