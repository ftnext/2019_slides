## Anaconda環境運用TIPS
### 〜Anacondaの環境構築について知る・答えられるようになる〜
#### PyCon JP 2019 (2019/09/17) nikkie

---

@snap[north]
### お前、誰よ (About nikkie)
@snapend

@snap[west span-50 text-center]

@ul[](false)
- ハンドルネーム nikkie （alias [@ftnext](https://twitter.com/ftnext)）
- 株式会社ユーザベース所属 データサイエンティスト（自然言語処理）
- ※本発表で示すのは、あくまで **個人の見解** です
@ulend

@snapend

@snap[east span-50 text-center]

スライドは↓から

![https://bit.ly/2lNRb10](pyconjp_anaconda_tips/assets/QR_slide_link.png)

`#pyconjp_5`

@snapend

Note:

所属組織や所属コミュニティを代表する見解ではなく

+++

@snap[north]
### 続：お前、誰よ (About nikkie)
@snapend

@snap[west span-50 text-center]

@ul[](false)
- PyCon JP 2019 スタッフ
- [みんなのPython勉強会](https://startpython.connpass.com/)スタッフ・4代目LT王子
- [Django Girls Tutorial](https://tutorial.djangogirls.org/ja/)翻訳や[Workshop](https://djangogirls.org/tokyo/)のコーチ
@ulend

@snapend

@snap[east span-50 text-center]

スライドは↓から

![https://bit.ly/2lNRb10](pyconjp_anaconda_tips/assets/QR_slide_link.png)

`#pyconjp_5`

@snapend

+++

### おことわり：Anaconda環境運用TIPSというタイトルですが

- Anacondaの秘技を伝授するわけでは **ありません**
	- nikkieが普段使うのはpython.orgからインストールしたPython
- Anacondaをオススメするトークではありません

+++

### 問題意識：伝わっていないAnacondaの使い方

- 初学者とAnacondaの接点（入門書やWeb記事）が増えている
- Pythonを人に教える中で、Anacondaの使い方が伝わっていないために発生した問題をたびたび解決

+++

### Anacondaの使い方が伝わっていなくて発生する問題例

あるパッケージをcondaコマンドでもpipコマンドでも管理したことが原因で、環境が壊れる

![tensorflowモジュールがimportできなくなりました](pyconjp_anaconda_tips/assets/destruted_env.png)

Note:

macOSで検証したところ、tensorflowモジュールがimportできなくなりました。
手順はAppendixで示します

+++

### 使い方が伝わっていない問題を解決するために

- Pythonを使う上でハマりにくい考え方をAnacondaにも適用
- Pythonでやりたいことをやるのに集中していただければ

+++

### トークの対象者

- メイン＝「知る」： **Anacondaを使っているPython初学者の方**
- サブ＝「答えられるようになる」：Anacondaについての質問に答えられなかったPython使いの皆さま

+++

### Anaconda環境運用TIPSのポイント

- パッケージ管理は`conda`と`pip`の二刀流
	- `conda`を積極的に。`pip`からは距離を置く
- `conda create`で環境を分けよう

この後説明するので、今は謎の呪文でも大丈夫です

+++

### 目次

- Anacondaを知ってみよう
- `conda`と`pip`を使い分けよう
- 仮想環境を使ってみよう

---

### 目次

- **Anacondaを知ってみよう**
- `conda`と`pip`を使い分けよう
- 仮想環境を使ってみよう

+++

### Anaconda

- PCにPythonをインストールする手段の1つ
- [JetBrainsのsurvey(2018)](https://www.jetbrains.com/research/python-developers-survey-2018/)では、22%が利用（複数回答で第3位）
- Pythonインタープリタと科学計算で使うパッケージ（後述）をまとめて配布

+++

AnacondaでPythonをインストールすると、科学計算で使うパッケージ(例：numpy)が使えるbase環境が整う

```shell
(base) $ python
Python 3.7.3 (default, Mar 27 2019, 22:11:17)
[GCC 7.3.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import numpy as np  # numpyのインストール不要
>>> np.__version__
'1.16.4'
```

Note:

- Anacondaを使わないPythonのインストールの場合は、ModuleNotFoundError

+++

### パッケージとは

<span class="eighty-percent-img">
![私たちはインターネットからパッケージ（Pythonファイルやそれを入れたフォルダのアーカイブファイル）をダウンロードし、インストールして使う](pyconjp_anaconda_tips/assets/pyconjp2019_images.001.png)
</span>

Note:

- 私たちはインターネットからパッケージをダウンロードし、インストールして使う
- パッケージ ≒ Pythonファイルやそれを入れたフォルダをアーカイブにしたファイル（ref: [Distribution Package](https://packaging.python.org/glossary/#term-distribution-package)）

+++

### パッケージの配布元は色々

<span class="eighty-percent-img">
![PyPIというリポジトリやAnacondaを提供する会社が管理するリポジトリがある](pyconjp_anaconda_tips/assets/pyconjp2019_images.002.png)
</span>

Note:

- PyPI
- Anaconda社が管理する

といったリポジトリがある

（Anaconda社はそういう会社名という説明になる。condaコマンドはOSS。商業利用もできる）

+++

### パッケージを管理するツール：パッケージマネージャ

<span class="eighty-percent-img">
![リポジトリからパッケージをダウンロードするにはパッケージマネージャというツールを使う](pyconjp_anaconda_tips/assets/pyconjp2019_images.003.png)
</span>

Note:

リポジトリからパッケージをダウンロードするにはパッケージマネージャというツールを使う

+++

### パッケージマネージャも複数ある

<span class="eighty-percent-img">
![Anacondaに付属するパッケージマネージャが`conda`、Anacondaを使わずにPythonをインストールした場合、パッケージマネージャは`pip`](pyconjp_anaconda_tips/assets/pyconjp2019_images.004.png)
</span>

Note:

- Anacondaに付属するパッケージマネージャが`conda`
- Anacondaを使わずにPythonをインストールした場合、パッケージマネージャは`pip`

+++

### `conda`と`pip`の比較

パッケージマネージャ | リポジトリ | パッケージ数
----- | ----- | -----
`pip` | PyPI | 多い（開発者に公開）
`conda` | repo.anaconda.com | 少ない（Anaconda社が管理）

---

### 目次

- Anacondaを知ってみよう
- **`conda`と`pip`を使い分けよう**
- 仮想環境を使ってみよう

+++

### `conda`はパッケージが少ない？

- 回答として[`conda-forge`](https://conda-forge.org/)：Anaconda社でなく、[コミュニティが管理するリポジトリ](https://docs.conda.io/projects/conda/en/latest/user-guide/concepts/channels.html?highlight=conda-forge#what-is-a-conda-channel)
- `--channel`(`-c`)オプション
	- `conda install scipy --channel conda-forge`
	- `--channel`を指定しない場合、Anaconda社管理リポジトリが対象

+++

### 最終手段`pip`

- `conda-forge`にもパッケージがない場合、[`pip`を使わざるを得ない](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-pkgs.html#installing-non-conda-packages)
- `pip install see`

>The differences between pip and conda packages cause certain unavoidable limits in compatibility but conda works hard to be as compatible with pip as possible.

Note:

seeは組み込み関数dirを読みやすくして置き換えるパッケージ

pipパッケージとcondaパッケージの違いが互換性に置いて避けられない制限をもたらす（Appendix参照）。
condaはpip互換となるように可能な限り対応している

↑形式が異なると言っている（次のスライドにつながる）

+++

### 危険：同名パッケージを`conda`でも`pip`でも管理する

- 形式の異なるパッケージ（Appendix参照）を、PC全体で見ると二重管理した状態
- 二重管理が積み重なることで、AnacondaのPython環境が壊れてしまう（冒頭の例）
- 参考：「[混ぜるな危険](http://onoz000.hatenablog.com/entry/2018/02/11/142347)」の話

+++

### `conda`側も改善してきているものの

- `conda`4.6以降では、`pip`でバージョンアップしたパッケージを`conda`で二重管理しない[改善例（ドキュメント）](https://docs.conda.io/projects/conda/en/latest/user-guide/configuration/pip-interoperability.html)
- 手元で検証したところ、併用によるリスクが絶対にないとは言い切れない

+++

### `conda`と`pip`の使い分け（方針）

1. Anaconda社のリポジトリや`conda-forge`のパッケージを使う（`pip install`は`conda install`に読み替える）
	- 極力`conda`を使うことで、`conda`で扱うパッケージと`pip`で扱うパッケージの重複を抑える
2. `conda`で見つからない場合だけ、`pip`を使う（`pip`は最終手段）

+++

![使い分け方針を図で示しています](pyconjp_anaconda_tips/assets/pyconjp2019_images.005.png)

+++

### なるべく`conda`コマンドを！

```shell
# condaで扱えるリポジトリでパッケージを検索
(base) $ conda search ... [-c conda-forge]
(base) $ conda install ... [-c conda-forge]
# condaで扱えるリポジトリからパッケージをアップデート
(base) $ conda update ... [-c conda-forge]
```

---

### 目次

- Anacondaを知ってみよう
- `conda`と`pip`を使い分けよう
- **仮想環境を使ってみよう**

+++

### Anacondaのbase環境のPythonを使っていくと

<span class="seventy-percent-img">
![アプリケーションAの開発のために `conda install LibFoo=1.0`](pyconjp_anaconda_tips/assets/pyconjp2019_images.006.png)
</span>

Note:

- アプリケーションAの開発のために `conda install LibFoo=1.0`

+++

### Anacondaのbase環境のPythonを使っていくと

<span class="seventy-percent-img">
![別のアプリケーションBの開発のために `conda install LibFoo=2.0`。base環境にはLibFooのバージョンの一方しか入らない。。](pyconjp_anaconda_tips/assets/pyconjp2019_images.007.png)
</span>

Note:

- 別のアプリケーションBの開発のために `conda install LibFoo=2.0`
- base環境にはLibFooのバージョンの一方しか入らない。。

+++

### 解決方法（Anacondaではない場合）

- 標準のPythonでは「仮想環境」が[案内](https://docs.python.org/ja/3/tutorial/venv.html)される
- 標準モジュールvenvを使用する（Python3.3以降）

+++

### venvのコマンド例（Anacondaではない場合）

```shell
$ python3 -m venv tutorial-env  # 仮想環境作成(Linux, macOS前提)
$ source tutorial-env/bin/activate  # 仮想環境有効化(Linux, macOS前提)
(tutorial-env) $ pip install scikit-learn
```

参考：[Python チュートリアル](https://docs.python.org/ja/3/tutorial/venv.html)、[Django Girls Tutorial](https://tutorial.djangogirls.org/ja/django_installation/)

+++

### venvによる解決方法（Anacondaではない場合）※Linux想定

<span class="seventy-percent-img">
![それぞれのアプリケーションの開発用ディレクトリの下に仮想環境のディレクトリを作り、そこにインストール。仮想環境どうしは独立させる](pyconjp_anaconda_tips/assets/pyconjp2019_images.008.png)
</span>

Note:

アプリケーションAの開発用ディレクトリの下に仮想環境のディレクトリを作る  
アプリケーションAに必要なモジュールは全てそこにインストール

アプリケーションBの開発用ディレクトリの下にも別の仮想環境のディレクトリを作る  
アプリケーションBに必要なモジュールは全てそこにインストール

+++

### Anaconda版「仮想環境」

- メリット：もし壊れてもその仮想環境を捨てるだけで済む
- Anacondaでもvenvを使うこともできる
	- base環境にインストールされた科学計算のパッケージを無視するため、Anaconda向きではないという考え
- よりAnacondaの機能を引き出すと考える方法を紹介：`conda create`

+++

### (案1) 仮想環境の使い方

tensorflowを使うための環境を作る

```shell
(base) $ conda create -n ml_tf python=3.6 jupyter tensorflow
(base) $ conda activate ml_tf
(ml_tf) $  # tensorflowを使った開発
(ml_tf) $ conda deactivate  # 開発終了後、base環境に戻す
(base) $
```

Note:

- tensorflowはbaseには入っていない
- `conda create`でPython3.6とnumpyが使える環境をmyenvという名前(`-n`)で作成
- `conda activate`で仮想環境myenvを有効にする
- `conda deactivate`で仮想環境myenvを無効にし、元の環境baseに戻す

+++

### (案2) 便利なbase環境をなるべく安全に使う

- 例：base環境に`pip`でパッケージを入れたい
- `conda create --clone base -n v2_base`
- うまく動かなかったら捨てればいい。base環境に影響はない

+++

### Anacondaにおける[仮想環境](https://conda.io/projects/conda/en/latest/user-guide/concepts/environments.html)

<span class="eighty-percent-img">
![base環境とは別に仮想環境用のディレクトリが/opt/conda/envsの下に作成され、そこに環境ごとにパッケージが入ります](pyconjp_anaconda_tips/assets/pyconjp2019_images.009.png)
</span>

Note:

base環境とは別に仮想環境用のディレクトリが/opt/conda/envsの下に作成され、そこに環境ごとにパッケージが入ります

---

### Anaconda環境運用TIPSで話したこと

- Anacondaを知ってみよう
- `conda`と`pip`を使い分けよう
- 仮想環境を使ってみよう

+++

### まとめ：Anaconda環境運用TIPS

- `conda`を積極的に使ってパッケージ管理を。`pip`は最終手段
- 仮想環境の考え方をAnacondaでも取り入れよう
	- `conda create`で環境を分けると便利
	- `conda create --clone`でbase環境を安全に使おう

+++

### 語り

- 繰り返しですが、Anacondaを薦めるトークではありません。思うに、環境構築の方法に優劣はない（Pythonでやりたいことができることが重要）
- 動いていることが重要。なんとしても今すぐ直さなきゃいけないわけじゃない。次に構築する時、もっとうまくやろう🐴

+++

### 参考資料

- [`conda`ドキュメント](https://docs.conda.io/projects/conda/en/latest/index.html)
- [各種一覧](https://docs.anaconda.com/anaconda/packages/pkg-docs/)

Note:

深く知りたい方はご確認ください

+++

### Appendix

- 動作検証環境
- `conda`コマンドを詳しく
- 盛り込みきれなかったこと

+++

### Special Thanks

- 練習に付き合ってくださった方々（職場、コミュニティ）
- 資料作成の場として利用させていただいたPythonのもくもく会（#pyhack, #rettypy）
- これまでPythonを教える機会をくださった方々
- PyCon JP 2018で「来年は登壇したい」と思った過去の自分
- 素敵なアニメでリフレッシュを支えてくださる京都アニメーション

+++

### ご清聴ありがとうございました

Appendixが続きます

---

### Appendix：動作検証環境

- 検証環境のバージョンを共有
- 環境破壊手順

+++

### 検証環境

- macOS 10.12.6、conda 4.6.11、anaconda=2019.07導入
- Dockerイメージ[continuumio/anaconda3](https://hub.docker.com/r/continuumio/anaconda3) タグ:2019.07, 5.1.0（ディレクトリ構造の確認にも使用）

+++

### 環境破壊手順（@macOS環境）

```shell
(base) $ conda create --clone base -n update_tf_test
(base) $ conda activate update_tf_test
(update_tf_test) $ conda install tensorflow=1.13.1
(update_tf_test) $ python
>>> import tensorflow
>>> exit()
(update_tf_test) $ pip install -U tensorflow
(update_tf_test) $ python
>>> import tensorflow
Illegal instruction: 4
(update_tf_test) $
```

---

### Appendix：`conda`コマンドを詳しく

- condaコマンド紹介（search, install）
- condaコマンドと仮想環境
- Anaconda環境の持ち運び
- `conda`と`pip`併用例（本編より詳しく）

+++

### `conda`でできること（一例）

- [`conda search scikit`](https://conda.io/projects/conda/en/latest/commands/search.html)：scikitを名前に含むパッケージを検索
- [`conda install scikit-rf`](https://conda.io/projects/conda/en/latest/commands/install.html)：パッケージのインストール
- マネージ（管理）するのはパッケージに限らず、Pythonのバージョンも管理できるのが特徴

+++

### [`conda create`](https://docs.conda.io/projects/conda/en/latest/commands/create.html)

- `conda create -n myenv python=3.7 numpy`
	- Python3.7とnumpyが使える環境をmyenvという名前で作成
- `conda create -n myenv2 anaconda`
	- base環境と同様に科学計算のパッケージが入った環境をmyenv2という名前で作成
	- base環境と共通のパッケージが入るが、最新バージョンになる（固定 [pinned](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-pkgs.html#preventing-packages-from-updating-pinning) も可能）

+++

### 仮想環境の操作

- 有効にする：`conda activate <仮想環境名>`
	- condaの4.6以降前提。4.6より前は[ドキュメント](https://conda.io/projects/continuumio-conda/en/latest/user-guide/getting-started.html#managing-environments)参照
- 無効にする：`conda deactivate`

+++

### 操作例

```shell
(base) $ conda create -n myenv python=3.7 numpy
(base) $ conda activate myenv
(myenv) $ python
Python 3.7.4 (default, Aug 13 2019, 20:35:49)
[GCC 7.3.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import numpy as np
>>> np.__version__
'1.16.4'
```

+++

### Anaconda環境の持ち運び

- 紹介した`conda create --clone`
- ymlファイルに[エクスポート](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#exporting-the-environment-yml-file)→[読み込み](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file)

+++

### [併用例](https://docs.conda.io/projects/conda/en/latest/user-guide/configuration/pip-interoperability.html)（imagesizeパッケージをpipでアップグレード）

```
(some_pip_test) $ conda --version
conda 4.7.10
(some_pip_test) $ conda list
# Name                    Version                   Build  Channel

imagesize                 1.0.0                    py37_0

(some_pip_test) $ pip install -U imagesize
(some_pip_test) $ conda list
# Name                    Version                   Build  Channel

imagesize                 1.1.0                    pypi_0    pypi

```

+++

### condaが4.6より前は併用できない

二重管理になってしまう（環境が壊れる要因に）

```
(some_pip_test) $ conda --version
conda 4.4.10
(some_pip_test) $ conda list
# Name                    Version                   Build  Channel

imagesize                 1.0.0                    py37_0

(some_pip_test) $ pip install -U imagesize
(some_pip_test) $ conda list
# Name                    Version                   Build  Channel

imagesize                 1.1.0                     <pip>
imagesize                 1.0.0                    py37_0  

```

+++

### 注意：併用の前に、[condaのバージョンを上げる](https://conda.io/projects/conda/en/latest/user-guide/getting-started.html#managing-conda)こと

`conda update conda`

(base)で実行する  
(base)に入っているパッケージのバージョンが上がる（必要であれば、先に紹介した固定方法）  
→imagesizeの例の二重管理の表示状態は解決される

---

### Appendix：盛り込みきれなかったこと

- Pythonのインストールと読み替え
- パッケージの形式の違い
- 調査が至らなかった事項

+++

### 補足：Pythonをインストールする手段は1つでOK

- AnacondaでPythonをインストールしたなら、python.orgなど他の手段は使う必要なし
- 本やWeb記事は、自分の環境に合わせて **読み替え** や **スキップ** しましょう
- 複数の手段でPythonをインストールしても、1つのコマンドラインから使えるPythonは1つだけ

+++

### パッケージの形式が異なる（[`conda`](https://docs.conda.io/projects/conda/en/latest/user-guide/concepts/packages.html#what-is-a-conda-package)／[`pip`](https://packaging.python.org/tutorials/packaging-projects/)）

<span class="seventy-percent-img">
![`conda`で扱うパッケージと`pip`で扱うパッケージの構成を比較](pyconjp_anaconda_tips/assets/pyconjp2019_images.010.png)
</span>

+++

### 調査が至らなかった事項

- 紹介したコマンドと、Anaconda NavigatorでのGUI操作の対応付け
- 環境分離ツールの"New Era" [pipenvはAnaconda環境でも使える](https://pipenv.readthedocs.io/en/latest/advanced/#pipenv-and-other-python-distributions)

+++

# EOF
