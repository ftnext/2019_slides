## 機械学習に興味ありますか？<br>Kaggle始めたいですか？<br>タイタニックでもいいですか？
#### サポーターズ勉強会 2019/10/24 nikkie

---

### Welcome!!

- Kaggle（というオンラインコミュニティ）の
- タイタニック（というコンペ）を
- 手を動かして体験（＝ハンズオン）していきます

Kaggleとタイタニックについてはこの後説明します

+++

### アンケート🙋‍

- Pythonでデータ分析経験あり
- PythonでWebや自動化経験あり
- Python以外でデータ分析経験あり

+++

### お前、誰よ（About nikkie）

- Alias @ftnext: [Twitter](https://twitter.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- エンジニア4年目。データサイエンティスト歴半年（Python）
- Pythonを教える活動（[Django Girls Tutorial](https://tutorial.djangogirls.org/ja/)翻訳など）やPyConJP 2019 スタッフ活動をしています
- アニメが好き（ユーフォ、アイマス）

+++

### 頼れるTAの皆さま👏

- shimakaze_softさん

---

### Kaggleのアカウント作成

**初めてKaggleに取り組む方** は作成をお願いします🙇

まず https://www.kaggle.com/account/login にアクセス

+++

<span class="eighty-percent-img">
![お好みの登録方法で進めてください（FB, Google, Yahoo, Email）](spz_Oct_titanic_handson4/assets/kaggle_register.png)
</span>

+++

### （参考）SMS認証

- 国コード +81 80-XXXX-XXXX（国コードを使うので、080の先頭の0は不要）
- 参考 [【機械学習】さあ、Kaggleを始めよう！ – 初心者向けPython Kernelとは](https://www.secat-blog.net/wordpress/kaggle-getting-started-python-kernel-for-beginners/)
- つまづいてしまった場合は、本スライドAppendix「Google Colaboratoryでの実行」を参照ください

---

### ハンズオン後の姿

- 機械学習の流れをつかんだ状態
- Kaggleのコンペでは何をやるか **体験** から分かっている

+++

### このハンズオンの限界

- 機械学習の概念を詳細に説明しません
- ディープラーニングには立ち入りません

まとめで情報提供します

+++

## Kaggleのアカウントはできましたか？

+++

### アジェンダ

- 導入：機械学習／Kaggle／タイタニック（10分）
- ハンズオン：手を動かしてタイタニックコンペに参加（35分）
- まとめ（10分）
- 質疑&もくもくタイム：精度向上に各自挑戦（10分）

---?include=spz_Oct_titanic_handson4/ML_kaggle_titanic.md

---

### すかすかタイタニックハンズオン

- 導入：機械学習／Kaggle／タイタニック（10分）
- <div class="kaggle-color-highlight">ハンズオン：手を動かしてタイタニックコンペに参加（35分）</div>
- まとめ（10分）
- 質疑&もくもくタイム：精度向上に各自挑戦（10分）

+++

### ハンズオン（35分）

1. 準備(10分)
2. 分析(10分)
3. 前処理、モデル作成、評価(10分)
4. もくもくに向けた説明（5分）

+++

### タイタニックコンペに参加

**全員** 操作をお願いします🙇

- ログイン後 https://www.kaggle.com/c/titanic にアクセス
- （コンペ一覧 https://www.kaggle.com/competitions から「titanic」で検索🔍してもよい）

+++

### タイタニックコンペにJoin

<span class="eighty-percent-img">
![「Join Competition」→「I Understand and Accept」](spz_Jan_titanic_handson/assets/join_titanic_competition.png)
</span>

+++

### ハンズオン

- ブラウザで以下のNotebook（≒ソースコード。Kernelとも呼ぶ）にアクセス
  - https://www.kaggle.com/ftnext/kaggle-spzcolab-201910
- Notebookを自分のアカウントにコピーして編集していきます

+++

### Notebookのコピー

![「・・・」→「Copy and Edit Kernel」をクリック](spz_Oct_titanic_handson4/assets/copy_and_edit_kernel.png)

+++

### 準備完了です！👍

<span class="ninety-percent-img">
![Notebookのコピーが編集できるようになりました](spz_Oct_titanic_handson4/assets/editting_notenook.png)
</span>

以降はNotebookを一緒に進めます

---

### Notebookで作った予測結果の提出方法

ハンズオンでは一緒に進めます

- 前提：submisson.csvを作成するセルまで実行が終わった状態
- 半角英数でタイトルをつけるのがオススメ（自分のNotebookを区別できる）
  - 例：「spzcolab_kaggle_20191024」

+++

### 1. Notebook上部の「Commit」をクリック

![](spz_Oct_titanic_handson4/assets/commit_notebook.png)

+++

### 処理が終わるのを待ちます

<span class="eighty-percent-img">
![](spz_Oct_titanic_handson4/assets/committing.png)
</span>

+++

### 2. Completeとなったら、リンクをクリック

<span class="ninety-percent-img">
![](spz_Oct_titanic_handson4/assets/open_version.png)
</span>

+++

### 3. outputという項目へ移動

<span class="seventy-percent-img">
![](spz_Oct_titanic_handson4/assets/kaggle_notebook_go_output.png)
</span>

※2のタブは **閉じない** でください

+++

### 4. Submit to Competition

![](spz_Oct_titanic_handson4/assets/kaggle_notebook_submission.png)

+++

### 初提出、お疲れさまでした🎉

+++

### 提出練習用データを試す

- 試しに提出することができる生死予測データ
- ここに提出したNotebookがあります（nikkieだけで試します）

+++

### 提出練習用データ

- 性能：0.76555 😳
- ロジックはシンプル。**女性が助かり、男性が死亡と予測**
- もくもくタイムで、提出練習用データのスコア超えに取り組みましょう

---

### もくもくタイムに向けて：0.76555超えを目指す

- Notebook下部のサンプルコードを組合せてみましょう
  - `"""`や`'''`の間のコードで置き換えます（例を示します）
- 先ほどCommitしたNotebookを編集しながら **上から再実行** します

+++

### Notebook再編集

<span class="seventy-percent-img">
![「Return to Editor」または「バツ（閉じるアイコン）」をクリックします](spz_Oct_titanic_handson4/assets/notebook_return_to_editor.png)
</span>

+++

### （参考）Notebook再実行 1/2

Notebookのタブを閉じてしまった方への案内です

![提出した画面で上部のNotebooksをクリック](spz_Oct_titanic_handson4/assets/submission_results_to_notebook.png)

+++

### （参考）Notebook再実行 2/2

![Your Recent Notebooksから先ほどのNotebookのEditをクリック](spz_Oct_titanic_handson4/assets/edit_your_recent_notebook.png)

+++

### （参考）Notebook再実行 補足1/2

![Recent Notebooksがない場合は、Your Workから先ほどのNotebookをクリック](spz_Oct_titanic_handson4/assets/select_your_notebooks.png)

+++

### （参考）Notebook再実行 補足2/2

![Editをクリック](spz_Oct_titanic_handson4/assets/edit_committed_notebook.png)

---?include=spz_Oct_titanic_handson4/summary.md

---

### 参考文献（ハンズオン準備に当たり）

- 『[Pythonによるあたらしいデータ分析の教科書](https://www.amazon.co.jp/dp/4798158348)』pydatatext（ベースにしました）
- PyData.Tokyo Tutorial [分析パート](https://github.com/PyDataTokyo/pydata-tokyo-tutorial-1/blob/master/pydatatokyo_tutorial_dh.ipynb) [モデル作成パート](https://github.com/PyDataTokyo/pydata-tokyo-tutorial-1/blob/master/pydatatokyo_tutorial_ml.ipynb)（タイタニックコンペを扱った先行事例）
- 『[PythonユーザのためのJupyter 実践 入門](https://www.amazon.co.jp/dp/4774192236/)』可視化で参照

+++

### ご清聴ありがとうございました
### ハンズオンお疲れさまでした！
Contact: [Twitter @ftnext](https://twitter.com/ftnext)

---

## 質疑&もくもくタイムです！

## 精度向上に挑戦💪

Pythonのサンプルコードを組合せて、試行錯誤しましょう

+++

## 0.76555超えた人🙋

---?include=spz_Oct_titanic_handson4/appendix.md
