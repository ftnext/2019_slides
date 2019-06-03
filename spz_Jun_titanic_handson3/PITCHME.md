## 【生配信】機械学習に興味ありますか？<br>Kaggle始めたいですか？<br>タイタニックでもいいですか？
#### サポーターズ勉強会 2019/06/04 nikkie

---

### アイスブレイク

Twitterにご自身のこと（Python歴やKaggle歴）を投稿してみてください😁

例「Pythonは入門者です。Kaggleは今回が初めてです #spzcolab」

+++

### お前、誰よ（About nikkie）

- Alias @ftnext: [Twitter](https://twitter.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- エンジニア4年目。4月から駆け出しデータサイエンティスト（Python）
- Pythonを教える活動（[Django Girls Tutorial](https://tutorial.djangogirls.org/ja/)翻訳など）やPyConJP 2019 スタッフ活動をしています
- アニメが好き（ユーフォ、アイマス）

---

### Kaggleのアカウント作成

**初めてKaggleに取り組む方** は作成をお願いします🙇

まず https://www.kaggle.com/account/login にアクセス

+++

<span class="eighty-percent-img">
![お好みの登録方法で進めてください（FB, Google, Yahoo, Email）](spz_Jan_titanic_handson/assets/kaggle_register.png)
</span>

できた方は「登録できました！ #spzcolab」ツイートお願いします🙇

+++

### （参考）SMS認証

- 国コード +81 80-XXXX-XXXX（国コードを使うので、080の先頭の0は不要）
- 参考 [【機械学習】さあ、Kaggleを始めよう！ – 初心者向けPython Kernelとは](https://www.secat-blog.net/wordpress/kaggle-getting-started-python-kernel-for-beginners/)
- つまづいてしまった場合は、本スライドAppendix「Google Colaboratoryでの実行」を参照ください

---

### 機械学習に興味ありますか？Kaggle始めたいですか？タイタニックでもいいですか？ って何よ

- Kaggle（というオンラインコミュニティ）の
- タイタニック（というコンペ）を
- 手を動かして体験（＝ハンズオン）

Kaggleとタイタニックについてはこの後説明します

+++

### ハンズオン後の姿

- 機械学習の流れをつかんだ状態
- Kaggleのコンペでは何をやるか **体験** から分かっている

+++

### このハンズオンの限界

- 機械学習の概念を詳細に説明しません
- ディープラーニングには立ち入りません

最後に参考資料を案内します

+++

## Kaggleのアカウントはできましたか？

+++

### アジェンダ

- 導入：機械学習／Kaggle／タイタニック（10分）
- ハンズオン：手を動かしてタイタニックコンペに参加（35分）
- まとめ（10分）
- 質疑&もくもくタイム：精度向上に各自挑戦（20分程度）

---?include=spz_Jun_titanic_handson3/ML_kaggle_titanic.md

---

### 【生配信】すかすかタイタニックハンズオン

- 導入：機械学習／Kaggle／タイタニック（10分）
- <div class="kaggle-color-highlight">ハンズオン：手を動かしてタイタニックコンペに参加（35分）</div>
- まとめ（10分）
- 質疑&もくもくタイム：精度向上に各自挑戦（20分程度）

+++

### ハンズオン（35分）

1. 準備(10分)
2. 分析(10分)
3. 前処理、モデル作成、評価(15分)

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

できた方は「タイタニックコンペに参加できました！ #spzcolab」ツイートお願いします🙇

+++

### ハンズオン

- ブラウザで以下のKernel（≒ソースコード）にアクセス
  - https://www.kaggle.com/ftnext/kaggle-spzcolab-201906
- Kernelを自分のアカウントにコピーします（フォークと言います）

+++

### Kernelのコピー

![「・・・」→「Fork Kernel」をクリック](spz_Jan_titanic_handson/assets/fork_kernel.png)

+++

### 準備完了です！👍

![Kernelのコピーが編集できるようになりました](spz_Jan_titanic_handson/assets/editting_kernel.png)

できた方は「フォークできました！ #spzcolab」ツイートお願いします🙇  
以降はKernelを一緒に進めます

+++

### Kernelの提出方法

ハンズオンでは一緒に進めます

- 前提：submisson.csvを作成するセルまで実行が終わった状態
- タイトルを変えるのがオススメ（自分のKernelを区別できる）
  - 例：「supporterz_kaggle_20190604」

+++

### 1. Kernel上部の「Commit」をクリック

![](spz_online_titanic_handson2/assets/commit_kernel.png)

+++

### 2. Completeとなったら、リンクをクリック

![](spz_online_titanic_handson2/assets/open_kernel_version.png)

+++

### 3. outputという項目へ移動

![](spz_Jan_titanic_handson/assets/kaggle_kernel_go_output.png)

※2のタブは **閉じない** でください

+++

### 4. Submit to Competition

![](spz_Jan_titanic_handson/assets/kaggle_kernel_submission.png)

+++

### 初提出、お疲れさまでした🎉

+++

### 提出練習用データを試す

- 試しに提出することができる生死予測データ
- ここに提出したkernelがあります（nikkieだけで試します）

+++

### 提出練習用データ

- 性能：0.76555 😳
- ロジックはシンプル。**女性が助かり、男性が死亡と予測**
- もくもくタイムで、提出練習用データのスコア超えに取り組みましょう

---?include=spz_Jun_titanic_handson3/summary.md

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

## もくもくタイムです！

## 精度向上に挑戦💪

Pythonのサンプルコードを組合せて、試行錯誤しましょう

+++

### 0.76555超えを目指す

- Kernel下部のサンプルコードを組合せてみましょう
  - `"""`の間のコードで置き換えます（例を示します）
- 先ほどCommitしたKernelを編集しながら **上から再実行** します

+++

### Kernel再編集

![「Return to Editor」をクリックします](spz_Jun_titanic_handson3/assets/kernel_return_to_editor.png)

+++

### （参考）Kernel再実行 1/3

Kernelのタブを閉じてしまった方への案内です

![提出した画面で上部のKernelsをクリック](spz_Jan_titanic_handson/assets/submission_results_to_kernel.jpg)

+++

### （参考）Kernel再実行 2/3

![Your Workから先ほどのKernelをクリック](spz_Jan_titanic_handson/assets/select_your_kernels.png)

+++

### （参考）Kernel再実行 3/3

![Editをクリック](spz_Jan_titanic_handson/assets/edit_committed_kernel.png)

+++

## 0.76555超えた人🙋

ぜひツイートを：「0.78出ました！ #spzcolab」

---?include=spz_Jun_titanic_handson3/appendix.md
