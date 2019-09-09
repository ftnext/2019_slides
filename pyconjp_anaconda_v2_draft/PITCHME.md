## Anaconda環境運用TIPS
### 〜Anacondaの環境構築について知る・答えられるようになる〜
#### PyCon JP 2019 (2019/09/17) nikkie

---

### お前、誰よ (About nikkie)

+++

### おことわり：TIPSですが

- Anacondaの秘技を伝授するわけでは **ありません**
	- nikkieの普段使いはpython.orgからインストールしたPython
- Anacondaをオススメするトークではありません
- 共有したいこと：Pythonを使う上でハマらない考え方

+++

### 問題意識：伝わっていないAnacondaの使い方

- Anacondaを案内するPython／機械学習の入門書が増加した印象（環境構築は簡単）
- 人に教える中でAnacondaの使い方が伝わっていないと感じた
- **Anacondaをハマらずに使って、Pythonでやりたいことをやってほしい**

+++

### 対象者

- メイン： **Anacondaを使っているPython初学者の方**
- サブ：Anacondaについての質問に答えられなかったPython使いの皆さん

+++

### Anaconda環境運用TIPSのポイント

- `conda`と`pip`は併用可能
	- ただし、`conda`のバージョンを上げる必要あり
- `conda create`で環境を分けよう

この後説明するので、今は謎の呪文でも大丈夫です

+++

### 目次

- Anacondaを知ってみよう
- condaとpipは併用可能
- 仮想環境を使ってみよう

---

### 目次

- **Anacondaを知ってみよう**
- condaとpipは併用可能
- 仮想環境を使ってみよう

+++

### Anaconda

- PCにPythonをインストールする手段の1つ
- Pythonインタープリタと科学計算で使うパッケージ（後述）をまとめて配布
- [JetBrainsのsurvey(2018)](https://www.jetbrains.com/research/python-developers-survey-2018/)では、22%が利用（複数回答で第3位）

+++

AnacondaでPythonをインストールすると、科学計算で使うパッケージ(例：numpy)がすぐに使える

```shell
(base) $ python
Python 3.7.3 (default, Mar 27 2019, 22:11:17)
[GCC 7.3.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import numpy as np  # numpyのインストール不要
>>> np.__version__
'1.16.4'
```

+++

### パッケージとは

- 私たちはインターネットからパッケージをダウンロードし、インストールして使う
- パッケージ ≒ Pythonファイルやそれを入れたフォルダをアーカイブにしたファイル（ref: [Distribution Package](https://packaging.python.org/glossary/#term-distribution-package)）

+++

### パッケージを管理するツール：パッケージマネージャ

- Anacondaに付属するパッケージマネージャが`conda`
- `conda`コマンドでパッケージのインストールやアップデートをする

+++

### `conda`でできること（一例）

- [`conda search scikit`](https://conda.io/projects/conda/en/latest/commands/search.html)：scikitを名前に含むパッケージを検索
- [`conda install scikit-rf`](https://conda.io/projects/conda/en/latest/commands/install.html)：パッケージのインストール
- マネージ（管理）するのはパッケージに限らず、Pythonのバージョンも管理できるのが特徴

デフォルトでは、Anaconda社管理下のパッケージが対象（[各種一覧](https://docs.anaconda.com/anaconda/packages/pkg-docs/)）。（Appendixへ）

+++

### `conda`以外のパッケージマネージャ

- Anacondaを使わずにPythonをインストールした場合、パッケージマネージャは`pip`
- `pip`コマンドでパッケージの検索やインストールなどが可能
- `pip`はデフォルトではPython Package Index(PyPI)にあるパッケージを対象にする

---

### 目次

- Anacondaを知ってみよう
- **condaとpipは併用可能**
- 仮想環境を使ってみよう

+++

## ポイント：condaとpipは[併用可能](https://docs.conda.io/projects/conda/en/latest/user-guide/configuration/pip-interoperability.html)

> conda now understands pip metadata more intelligently.

- ただしcondaのバージョンが4.6.0以降（conda --version）

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

## 重要：conda 4.6以降は、condaとpipは併用可能

忘れずにお持ち帰りください

---

### 目次

- Anacondaを知ってみよう
- condaとpipは併用可能
- **仮想環境を使ってみよう**

+++

### Pythonを使っていくと出会う問題

- Anacondaのbase環境のPythonでアプリケーション開発
- アプリケーションAの開発には、LibFooパッケージのバージョン1.0が必要
- 別のアプリケーションBの開発には、LibFooパッケージのバージョン2.0が必要
- base環境にはLibFooが1つのバージョンしか入らない。。

+++

TODO：1つのバージョンしか入らないことについてコマンドラインの例を入れる

+++

### 解決方法

- 解決方法として、標準のPythonでは「仮想環境」が[案内](https://docs.python.org/ja/3/tutorial/venv.html)される
- 標準モジュールvenvを使用する（Python3.3以降）

+++

### venvによる解決方法（TODO：あとで図にしたい）

アプリケーションAの開発用ディレクトリの下に仮想環境のディレクトリを作る  
アプリケーションAに必要なモジュールは全てそこにインストール

アプリケーションBの開発用ディレクトリの下にも別の仮想環境のディレクトリを作る  
アプリケーションBに必要なモジュールは全てそこにインストール

+++

### venvのコマンド例

```shell
$ python3 -m venv tutorial-env  # 仮想環境作成(Linux, macOS前提)
$ source tutorial-env/bin/activate  # 仮想環境有効化(Linux, macOS前提)
(tutorial-env) $ pip install scikit-learn
```

参考：[Python チュートリアル](https://docs.python.org/ja/3/tutorial/venv.html)、[Django Girls Tutorial](https://tutorial.djangogirls.org/ja/django_installation/)

+++

### Anaconda版「仮想環境」

- Anacondaでもvenvを使うこともできる
- よりAnacondaの機能を引き出すと考える方法を紹介：`conda create`

+++

### [`conda create`](https://docs.conda.io/projects/conda/en/latest/commands/create.html)

- `conda create -n myenv python=3.7 numpy`
	- Python3.7とnumpyが使える環境をmyenvという名前で作成
- `conda create -n myenv2 anaconda`
	- base環境と同様に科学計算のパッケージが入った環境をmyenv2という名前で作成

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

---

### まとめ：Anaconda環境運用TIPS

- condaを4.6以降にアップデート
- `conda create`で環境を分けると便利
- 分けた環境の中でcondaとpipのいいとこどりを

+++

### 語り

- 繰り返しですが、Anacondaを薦めるトークではありません。思うに、環境構築の方法に優劣はない（Pythonでやりたいことができることが重要）
- 動いていることが重要。なんとしても今すぐ直さなきゃいけないわけじゃない。次に構築する時、もっとうまくやろう🐴

+++

### Special Thanks

- 練習に付き合ってくださった方々（職場、コミュニティ）
- 資料作成の場として利用させていただいたPythonのもくもく会（#pyhack, #rettypy）
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

チャンネル

- チャンネル（TODO：要説明）からパッケージを検索・インストール・アップデート
- デフォルト、コミュニティ管理のチャンネルも対象にできる

+++

環境の持ち運び方法（ファイルからの読み込みやclone）

+++

### おまけ：環境切り分けのNew Era

pipenvまたはpoetryを紹介
