### Appendix

- ハンズオンソースコードへの補足情報
- ささやかな **応用コンテンツ**
- タイタニック号沈没事故について（分析の裏付け）
- Google Colaboratoryでの実行

+++

### （参考）`train_test_split` 1/3

<span class="seventy-percent-img">
![モデル作成用データをランダムに2つに分ける](spz_Jan_titanic_handson/assets/201901kaggel_talk.008.png)
</span>

+++

### （参考）`train_test_split` 2/3

<span class="seventy-percent-img">
![2つに分けた片方からモデルを作る](spz_Jan_titanic_handson/assets/201901kaggel_talk.009.png)
</span>

+++

### （参考）`train_test_split` 3/3

<span class="seventy-percent-img">
![2つに分けた残りでモデルの性能を評価する](spz_Jan_titanic_handson/assets/201901kaggel_talk.010.png)
</span>

+++

### さらに工夫できる 1/2

- 連続値（AgeやFare）をいくつかのカテゴリに分ける
- 年齢の小さいところで助かっている（4歳以下）
  - → Nameを加工してTitle

+++

### さらに工夫できる 2/2

- 特徴量を作る
  - Aloneかどうか（SibSpとParchを加工する）
  - Pclass と Age（カテゴリ）の積
- 詳しくは[可視化の参考にしたkernel参照](https://www.kaggle.com/startupsci/titanic-data-science-solutions)

---

### ささやかな応用コンテンツ

準備中

---

### タイタニック号沈没事故

- Wikipedia [タイタニック号沈没事故](https://ja.m.wikipedia.org/wiki/%E3%82%BF%E3%82%A4%E3%82%BF%E3%83%8B%E3%83%83%E3%82%AF%E5%8F%B7%E6%B2%88%E6%B2%A1%E4%BA%8B%E6%95%85)
- 1912年4月の海難事故
- イギリス・サウサンプトンからアメリカ・ニューヨークへの航海中、氷山に衝突
- 2224人を乗せており、1513人(**68%**)が死亡

+++

### （おまけ）タイタニック裏話

先のWikipediaを確認したところ・・・

- 救命ボートの数が全員分ない -> 女性と子供優先
- 客室係がさばく乗客の数が等級によって違う
- 三等船室からデッキまでたどり着けず（客室係と言葉が通じない問題）

---

### Google Colaboratoryでの実行

- Kaggleが使えない場合のハンズオン用に用意
- Googleアカウントを持っている前提
- 用意したサンプルコードはColaboratoryでも動かすことができる

+++

### Google Colaboratoryでの実行手順

1. https://colab.research.google.com/ にアクセス
2. GitHubリポジトリ https://github.com/ftnext/spzcolab_titanic の中のノートブックを開く(続くスライドで説明)

+++

### ノートブックを開く 1/2

![GitHubのタブを選び、https://github.com/ftnext/spzcolab_titanic と入力](spz_Jan_titanic_handson/assets/colab_select_notebook.png)

+++

### ノートブックを開く 2/2

![ノートブック(.ipynb)のリンクをクリック](spz_Jun_titanic_handson3/assets/colab_select_notebook3.png)

+++

### セル実行時 1/2

![セルを初めて実行したときの警告は「このまま実行」を選択](spz_Jan_titanic_handson/assets/colab_run_cell.png)

+++

### セル実行時 2/2

![続くすべてのランタイムをリセットは「はい」を選択](spz_Jan_titanic_handson/assets/colab_run_cell2.png)

+++

# EOF
