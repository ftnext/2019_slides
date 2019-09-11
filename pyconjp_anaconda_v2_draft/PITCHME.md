## Anaconda環境運用TIPS
### 〜Anacondaの環境構築について知る・答えられるようになる〜
#### PyCon JP 2019 (2019/09/17) nikkie

---

### お前、誰よ (About nikkie)

- ハンドルネーム nikkie （alias [@ftnext](https://twitter.com/ftnext)）
- 株式会社ユーザベース所属 データサイエンティスト（※本発表は **個人の見解** です）
- PyCon JP 2019 スタッフ、みんなのPython勉強会スタッフ・4代目LT王子
- Django Girls Tutorial翻訳やWorkshopのコーチ

+++

### おことわり：Anaconda環境運用TIPSというタイトルですが

- Anacondaの秘技を伝授するわけでは **ありません**
	- nikkieが普段使うのはpython.orgからインストールしたPython
- Anacondaをオススメするトークではありません

+++

### 問題意識：伝わっていないAnacondaの使い方

- 初学者とAnacondaの接点（入門書やWeb記事）が増えている
- 教える中で、Anacondaの使い方が伝わっていないために発生した問題をたびたび解決
- このトークでは、Pythonを使う上でハマりにくい考え方をAnacondaにも適用 → Pythonでやりたいことをやるのに集中できるように

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
- 2本の刀：`conda`と`pip`
- 仮想環境を使ってみよう

---

### 目次

- **Anacondaを知ってみよう**
- 2本の刀：`conda`と`pip`
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

### 補足：Pythonをインストールする手段は1つでOK

- AnacondaでPythonをインストールしたなら、python.orgなど他の手段は使う必要なし
- 本やWeb記事は読み替えましょう
- 複数の手段でPythonをインストールしても、1つのコマンドラインから使えるPythonは1つだけ

+++

### パッケージとは

![私たちはインターネットからパッケージ（Pythonファイルやそれを入れたフォルダのアーカイブファイル）をダウンロードし、インストールして使う](pyconjp_anaconda_v2_draft/assets/pyconjp2019_images.001.png)

Note:

- 私たちはインターネットからパッケージをダウンロードし、インストールして使う
- パッケージ ≒ Pythonファイルやそれを入れたフォルダをアーカイブにしたファイル（ref: [Distribution Package](https://packaging.python.org/glossary/#term-distribution-package)）

+++

### パッケージの配布元は色々

![PyPIというリポジトリやAnacondaを提供する会社が管理するリポジトリがある](pyconjp_anaconda_v2_draft/assets/pyconjp2019_images.002.png)

Note:

- PyPI
- Anaconda社（Anacondaの提供元）管理

+++

### パッケージを管理するツール：パッケージマネージャ

![リポジトリからパッケージをダウンロードするにはパッケージマネージャというツールを使う](pyconjp_anaconda_v2_draft/assets/pyconjp2019_images.003.png)

Note:

リポジトリからパッケージをダウンロードするにはパッケージマネージャというツールを使う

+++

### パッケージマネージャも複数ある

![Anacondaを使わずにPythonをインストールした場合、パッケージマネージャは`pip`、Anacondaに付属するパッケージマネージャが`conda`](pyconjp_anaconda_v2_draft/assets/pyconjp2019_images.004.png)

パッケージの形式が異なるのが一因（後述）

Note:

- Anacondaを使わずにPythonをインストールした場合、パッケージマネージャは`pip`
- Anacondaに付属するパッケージマネージャが`conda`（コマンド）

+++

### `conda`と`pip`の比較

パッケージマネージャ | リポジトリ | パッケージ数
----- | ----- | -----
`pip` | PyPI | 多い（開発者に公開）
`conda` | repo.anaconda.com | 少ない（Anaconda社が管理）

---

### 目次

- Anacondaを知ってみよう
- **2本の刀：`conda`と`pip`**
- 仮想環境を使ってみよう

+++

### `conda`はパッケージが少ない？

- 回答：[`conda-forge`](https://conda-forge.org/)
- PyPIのAnacondaにおけるPyPIのようなリポジトリ ref:[docs](https://docs.conda.io/projects/conda/en/latest/user-guide/concepts/channels.html?highlight=conda-forge#what-is-a-conda-channel)
- デフォルトのAnaconda社管理リポジトリ以外を対象にする際は`--channnel`(`-c`)オプション：`conda install scipy --channel conda-forge`

+++

### 最終手段`pip`

- `conda-forge`にもパッケージがない場合、`pip`を使わざるを得ない ref:[docs](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-pkgs.html#installing-non-conda-packages)
- `pip install see`

>The differences between pip and conda packages cause certain unavoidable limits in compatibility but conda works hard to be as compatible with pip as possible.

Note:

pipパッケージとcondaパッケージの違いが互換性に置いて避けられない制限をもたらす。
condaはpip五巻となるように可能な限り対応している

+++

### 気にしたい：パッケージの形式が異なる

TODO：フォルダ構造を横に並べて見せたい

ref: [`conda`で扱うパッケージ](https://docs.conda.io/projects/conda/en/latest/user-guide/concepts/packages.html#what-is-a-conda-package)、[`pip`で扱うパッケージ](https://packaging.python.org/tutorials/packaging-projects/)

+++

### `conda`側も改善してきているものの

- ドキュメントに`conda`4.6以降で`pip`と併用可能を示す[例](https://docs.conda.io/projects/conda/en/latest/user-guide/configuration/pip-interoperability.html)
- 手元で検証したところ、併用によるリスクが絶対にないとは言い切れない

+++

### `conda`と`pip`の使い分け（方針）

1. Anaconda社のリポジトリや`conda-forge`のパッケージを使う（`pip install`は`conda install`に読み替える）
	- 極力`conda`を使うことで、`conda`向けパッケージと`pip`向けパッケージの重複を抑える
2. `conda`で見つからない場合だけ、`pip`を使う（`pip`は最終手段）

+++

![](pyconjp_anaconda_v2_draft/assets/pyconjp2019_images.005.png)

+++

### なるべく`conda`コマンドを！

```shell
(base) $ conda search ...  # conda向けリポジトリでパッケージを検索
(base) $ conda install ...
(base) $ conda update ...  # conda向けリポジトリからパッケージをアップデート
```

---

### 目次

- Anacondaを知ってみよう
- 2本の刀：`conda`と`pip`
- **仮想環境を使ってみよう**

+++

### Anacondaのbase環境のPythonを使っていくと

![アプリケーションAの開発のために `conda install LibFoo=1.0`。別のアプリケーションBの開発のために `conda install LibFoo=2.0`。base環境にはLibFooのバージョンの一方しか入らない。。](pyconjp_anaconda_v2_draft/assets/pyconjp2019_images.006.png)

Note:

- アプリケーションAの開発のために `conda install LibFoo=1.0`
- 別のアプリケーションBの開発のために `conda install LibFoo=2.0`
- base環境にはLibFooのバージョンの一方しか入らない。。

+++

### 解決方法（Anacondaではない場合）

- 標準のPythonでは「仮想環境」が[案内](https://docs.python.org/ja/3/tutorial/venv.html)される
- 標準モジュールvenvを使用する（Python3.3以降）

+++

### venvによる解決方法（Anacondaではない場合）

![それぞれのアプリケーションの開発用ディレクトリの下に仮想環境のディレクトリを作り、そこにインストール。仮想環境どうしは独立させる](pyconjp_anaconda_v2_draft/assets/pyconjp2019_images.007.png)

Note:

アプリケーションAの開発用ディレクトリの下に仮想環境のディレクトリを作る  
アプリケーションAに必要なモジュールは全てそこにインストール

アプリケーションBの開発用ディレクトリの下にも別の仮想環境のディレクトリを作る  
アプリケーションBに必要なモジュールは全てそこにインストール

+++

### venvのコマンド例（Anacondaではない場合）

```shell
$ python3 -m venv tutorial-env  # 仮想環境作成(Linux, macOS前提)
$ source tutorial-env/bin/activate  # 仮想環境有効化(Linux, macOS前提)
(tutorial-env) $ pip install scikit-learn
```

参考：[Python チュートリアル](https://docs.python.org/ja/3/tutorial/venv.html)、[Django Girls Tutorial](https://tutorial.djangogirls.org/ja/django_installation/)

+++

### Anaconda版「仮想環境」

- Anacondaでもvenvを使うこともできる
	- Anacondaに同梱された科学計算向けパッケージを無視するため、Anaconda向きではないという考え
- よりAnacondaの機能を引き出すと考える方法を紹介：`conda create`
- もし壊れてもその環境を捨てるだけで済む

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

### (案2) 便利なbase環境をなるべく安全に使う TODO検証

- 例：base環境に`pip`でパッケージを入れたい
- `conda create --clone base`
- うまく動かなかったら捨てればいい。base環境に影響はない

---

### まとめ：Anaconda環境運用TIPS

- `conda`を積極的に使ってパッケージ管理を。`pip`は最終手段
- 仮想環境の考え方をAnacondaでも取り入れよう
	- `conda create`で環境を分けると便利
	- `conda clone`でbase環境を安全に使おう

+++

### 語り

- 繰り返しですが、Anacondaを薦めるトークではありません。思うに、環境構築の方法に優劣はない（Pythonでやりたいことができることが重要）
- 動いていることが重要。なんとしても今すぐ直さなきゃいけないわけじゃない。次に構築する時、もっとうまくやろう🐴

+++

### Appendix

TODO：目次

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

Appendix

- 検証環境のバージョンを共有

+++

condaコマンドでできること

+++

### `conda`でできること（一例）

- [`conda search scikit`](https://conda.io/projects/conda/en/latest/commands/search.html)：scikitを名前に含むパッケージを検索
- [`conda install scikit-rf`](https://conda.io/projects/conda/en/latest/commands/install.html)：パッケージのインストール
- マネージ（管理）するのはパッケージに限らず、Pythonのバージョンも管理できるのが特徴

デフォルトでは、Anaconda社管理下のパッケージが対象（[各種一覧](https://docs.anaconda.com/anaconda/packages/pkg-docs/)）。（Appendixへ）

+++

### [`conda create`](https://docs.conda.io/projects/conda/en/latest/commands/create.html)

- `conda create -n myenv python=3.7 numpy`
	- Python3.7とnumpyが使える環境をmyenvという名前で作成
- `conda create -n myenv2 anaconda`
	- base環境と同様に科学計算のパッケージが入った環境をmyenv2という名前で作成
	- base環境と共通のパッケージが入るが、最新バージョンになる（固定も可能 TODOドキュメント）

+++

### 仮想環境の操作

- 有効にする：`conda activate <仮想環境名>`
	- condaの4.6以降前提。4.6より前は[ドキュメント](https://conda.io/projects/continuumio-conda/en/latest/user-guide/getting-started.html#managing-environments)参照
- 無効にする：`deactivate`

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

### conda createの挙動

ROOT_DIRの/envs下に仮想環境に対応するディレクトリが作成される [ref](https://conda.io/projects/conda/en/latest/user-guide/concepts/environments.html)  
それぞれのディレクトリの下にパッケージがインストールされている

```
/opt/conda/envs/
├── myenv
├── myenv2
└── some_pip_test
```

+++

### 併用例（imagesizeパッケージをpipでアップグレード）

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

### condaのバージョンを上げる

`conda update conda`

(base)で実行する  
(base)に入っているパッケージのバージョンが上がる（固定する方法もある）  
二重管理の表示状態が解決された（見た目の変更だけの可能性）

https://conda.io/projects/conda/en/latest/user-guide/getting-started.html#managing-conda

+++

チャンネル

- チャンネル（TODO：要説明）からパッケージを検索・インストール・アップデート
- デフォルト、コミュニティ管理のチャンネルも対象にできる

+++

環境の持ち運び方法（ファイルからの読み込みやclone）

+++

### おまけ：環境切り分けのNew Era

pipenvまたはpoetryを紹介
