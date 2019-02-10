# pandas vor!
### pandasの基礎は奥深いいぞ
#### みんなのPython勉強会#42 (2019/02/13) nikkie

---

### LT: pandas vor!

- 意味：「pandas前進！」
- pandasを使ったデータ分析を前に進めるため、基礎を確認 → 知ったことを共有します

+++

### About nikkie

- Alias @ftnext: [Twitter](https://twitter.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- 2018/09〜 stapy 4代目LT王子
- 1年前の2018/02が[stapyにおけるはじまりのLT](https://speakerdeck.com/ftnext/begin-pandas)です

+++

### 最近のアウトプット

- Django基礎ハンズオン（eLV勉強会）
  - part1：[2019/01/24](https://elv.connpass.com/event/114810/)、part2：[2019/02/14](https://elv.connpass.com/event/119181/)
- Kaggleタイタニックハンズオン（サポーターズ勉強会）
  - 第1回：[2019/01/30](https://supporterzcolab.com/event/677/)、第2回：2019/03

+++

### LT: pandas vor!

1. indexとcolumn
2. 複数列選択でリストを渡し損ねたときのエラー
3. nan、この特別な存在

---

### LT: pandas vor!

1. indexとcolumn
2. DataFrameから複数列選択
3. nan、この特別な存在

+++

### indexとcolumn

![indexとcolumnの例：タイタニックの乗客属性データ](stapy_Feb_pandas_basics/assets/df_index_and_column.png)

+++

### indexとcolumn

- indexは0, 1, 2, ... の部分
- columnは列名の部分

+++

### `df.drop(['Ticket', 'Cabin'], axis=1)`

カラムの中から該当する名前を削除と解釈できる

![カラムの中からTicketとCabinを削除](stapy_Feb_pandas_basics/assets/drop_specified_column.png)

---

### LT: pandas vor!

1. indexとcolumn
2. DataFrameから複数列選択
3. nan、この特別な存在

+++

### DataFrameから複数列選択

- カラム名のリストを渡す：`df[['columnA', 'columnB']]`
- リストで渡し損ねるとKeyError：`df['columnA', 'columnB']`

+++

### なぜKeyError？

- 'columnA', 'columnB'はタプルとして解釈される
- ('columnA', 'columnB') というカラムを探すが、見つからない

```console
>>> 2, 3
(2, 3)
```

+++

### 試してみる 1/2

DataFrame `prince`

name | alias | (name, alias)
----- | ----- | -----
denzow | denzowill | (denzow, denzowill)
nao_y | NaoY_py | (nao_y, NaoY_py)
Swall0w | Swall0wTech | (Swall0w, Swall0wTech)
nikkie | ftnext | (nikkie, ftnext)

+++

### 試してみる 2/2

`prince['name', 'alias']`

```
0       (denzow, denzowill)
1          (nao_y, NaoY_py)
2    (Swall0w, Swall0wTech)
3          (nikkie, ftnext)
Name: (name, alias), dtype: object
```

---

### LT: pandas vor!

1. indexとcolumn
2. DataFrameから複数列選択
3. nan、この特別な存在

+++

### nanの異常性

- 自分自身と比較してFalse😧
- nan（欠損）の検出は`isnull()`を使いましょう

```python
import numpy as np
np.nan == np.nan
# False
```

---

### Why LT:pandas vor!

なぜこのLTをするに至ったかを共有

+++

### 読み始めました

[pandasクックブック](http://www.asakura.co.jp/books/isbn/978-4-254-12242-8/)(2019 朝倉書店)

![pandasクックブック 書影](http://www.asakura.co.jp/goods_img/115751.jpg)

+++

### どれもpandasクックブックで知りました

1. indexとcolumn（レシピ1）
2. DataFrameから複数列選択（レシピ11）
3. nan、この特別な存在 （レシピ17）

+++

### pandasクックブック

- 1-2章でずいぶん知らないことがあった
- 全9章あり、**データ分析の力を鍛えられそう** でワクワク😆

+++

### まとめ：pandas vor!

- pandasを使ったデータ分析を前進させるために基礎を確認
- 知らないことが多く、pandasの基礎の奥深さを実感
- 『pandasクックブック』でpandas基礎力磨きに取り組んでいきます

+++

### ご清聴ありがとうございました。
## pandas vor!
Contact: [Twitter @ftnext](https://twitter.com/ftnext)
