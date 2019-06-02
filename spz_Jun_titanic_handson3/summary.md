### 【生配信】すかすかタイタニックハンズオン

- 導入：機械学習／Kaggle／タイタニック（10分）
- ハンズオン：手を動かしてタイタニックコンペに参加（30分）
- もくもくタイム：精度向上に各自挑戦（5分）
- <div class="kaggle-color-highlight">まとめ（10分）</div>

+++

### まとめ

- ハンズオンの振り返り
- 機械学習の学び方案
- Kaggleの取り組み方案

+++

### 再掲：機械学習の全体像

<span class="seventy-percent-img">
![問題設定→データ収集→分析→**前処理→モデル作成→モデル評価**→運用](spz_Jan_titanic_handson/assets/201901kaggel_talk.003.png)
</span>

+++

### 体験したこと

1. 分析（生存と関係するデータ項目を洗い出した）
2. 前処理（データは抜けや形式のために、そのままでは機械学習に持ち込めない）
3. モデル作成（わずか1行！）
4. モデル評価

---

### 機械学習の取り組み方案

- **機械学習の考え方** を学ぶ
- Pythonを学ぶ
- Pythonで使うツール（パッケージ）を学ぶ

+++

### 機械学習の考え方を学ぶ

学習用データの分割などの **考え方** を学びましょう（注：数学を学ぶのではありません）

- 『[Pythonによるあたらしいデータ分析の教科書](https://www.amazon.co.jp/dp/4798158348)』(pydatatext) 2018/09
- 『[東京大学のデータサイエンティスト育成講座](https://www.amazon.co.jp/dp/4839965250/)』 2019/03

毎月のように機械学習本が出ているので、書店で見比べをオススメします

+++

### Pythonを学ぶ

- 入門書は豊富（毎月のように新刊が出るので、書店で見比べをオススメ）
- [公式チュートリアル](https://docs.python.org/ja/3/tutorial/index.html)(無料)
- 有料のオンライン教材：[PyQ](https://pyq.jp/)など

+++

### Pythonで使うツール（パッケージ）を学ぶ

- まずはpandas（分析・前処理）とscikit-learn（モデル作成・評価）
- 機械学習の考え方を学ぶで挙げた2冊でも入門できます
- 『[Pythonではじめる機械学習](https://www.amazon.co.jp/dp/4873117984/)』scikit-learn（実践）
- 『[pandasクックブック](https://www.amazon.co.jp/dp/425412242X)』pandas（実践）

+++

### ディープラーニングを学ぶ

- Kaggelのコンペでは、ディープラーニングを使うことも多い
- ディープラーニングのパッケージ：TensorFlow, PyTorch, Chainer, ...
- 私は[TensorFlowチュートリアル](https://www.tensorflow.org/tutorials/)で学びました（機械学習の考え方も学べます）

+++

### （参考）ハンズオンがちょっと難しかったという方向け

[Udemy はじめてのAI](https://www.udemy.com/google-jp-ai/)

- Google佐藤さんによる無料講義
- AI、機械学習、ディープラーニングの関係性がつかめます

+++

### （参考）nikkieのアウトプット関連

- このハンズオンの学生向けバージョンの[Kernel](https://www.kaggle.com/ftnext/kaggle-spzcolab-online)
- 技術書典6で、少し進んだ内容を[合同誌](https://supporterz.booth.pm/items/1315417)でアウトプット（交差検証、グリッドサーチ）
- アウトプットの元の[PyData.Tokyo Tutorial](https://github.com/PyDataTokyo/pydata-tokyo-tutorial-1)

---

### Kaggleの取り組み方案

- Kaggleで機械学習を学ぶ
- Kaggleのコンペに参加する

+++

### Kaggleで学ぶ

- 「機械学習を学ぶにはKaggleがいい」と言われる
- うまく行った手法はKernelに公開される文化がある
- 探す→まねる→工夫する
  - 探す：https://www.kaggle.com/c/titanic/kernels

+++

### Kernelを探す

![投票数が多いもの、またはスコアが高いものに注目しましょう。また、言語で絞り込めます](spz_Mar_titanic_handson2/assets/titanic_kernels.png)

+++

### Kaggleのコンペに参加する

- 自分が興味をもてる開催中のコンペに参加（タイタニックで基礎固めでもOK）
- 評価が高いKernel、スコアが高いKernelの写経からスタート
- 探す→まねる→工夫する で 順位を上げることに取り組みましょう
- ref: 2018/05 [[入門者向け] Kaggle入門](https://supporterzcolab.com/event/380/)

+++

### Kaggleをバリバリやっていきたい方へ

注：Kaggleをバリバリやっていない立場からの見解です

- 興味あるコンペのスコアを上げるために、必要なところだけつまみ食い学習
- Kagglerから情報入手（例 [カレーちゃん](https://twitter.com/currypurin)さんによる[チュートリアル](https://note.mu/currypurin/n/nf390914c721e)）
- 一番重要と思うのは、時間の確保（他は手を出せなくなる）
