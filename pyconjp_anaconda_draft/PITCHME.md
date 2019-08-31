## Anaconda環境運用TIPS
### 〜Anacondaの環境構築について知る・答えられるようになる〜
#### PyCon JP 2019 (2019/09/17) nikkie

---

### お前、誰よ (About nikkie)

- ハンドルネーム nikkie （alias [@ftnext](https://twitter.com/ftnext)）
- PyCon JP 2019 スタッフ
- Django Girls Workshopコーチ、#pycamp TA
- 〇〇所属のデータサイエンティスト（※本発表は個人の見解です）

+++

### Anaconda環境運用TIPSのスタンス

- Anacondaを薦めるトークではない
- 思うに、環境構築の方法に優劣はない（Pythonでやりたいことができればいい）

+++

### 問題意識

- Anacondaを薦める入門書が増えている
- 一方、Anacondaを用いているにも関わらず、`pip install`を多用する危険な環境構築記事も散見される
- コーチとして、危険な環境構築方法に起因する問題解決もしばしば経験

+++

### Anaconda環境運用TIPSのスタンス

- Anacondaを薦めるトークではない（大事なことなので）
- **リスクの少ない環境構築方法** を勧めたい

+++

### 持ち帰ってほしいこと

- Anacondaの環境を切り分けよう（`conda create -n myenv python=3.7`）
- パッケージをインストールして使うまでの概要をつかもう

+++

### 目次

- Pythonが使えるとは？
- パッケージとは？
- 環境の分離とは？
- Anacondaで環境を分離する

---

### 目次

- Pythonが使えるとは？
- パッケージとは？
- 環境の分離とは？
- Anacondaで環境を分離する

---

### 目次

- Pythonが使えるとは？
- パッケージとは？
- 環境の分離とは？
- Anacondaで環境を分離する

+++

### そもそも`python`が使える状態とは？

- Pythonインタープリタ（バイナリ）が手元のPCに入っている
- 環境変数PATHが設定されている

+++

### 環境変数PATHの説明

+++

### Pythonインタープリタの入手方法は複数ある

- PSFのページからインストール（標準のCPython）
- Anaconda（別種）
- 他に、macOSのhomebrewやLinux(Debian系)のaptでの導入

+++

### Anaconda

- Pythonと科学計算に必要な「パッケージ」をセットにして配布
- 「パッケージマネージャ」`conda`

「」付きの単語は後述します

ref: https://docs.python.org/ja/3/using/windows.html#alternative-bundles

---

### 目次

- Pythonが使えるとは？
- パッケージとは？
- 環境の分離とは？
- Anacondaで環境を分離する

+++

### aisatsu.py

```python
def aisatsu():
    print('こんにちは PyCon JP 2019 🐍')
```

### `import`

- 自分が書いたPythonのプログラムをimportして使える
- `import aisatsu; aisatsu.hello()`

+++

### モジュール

- Pythonのプログラム（.pyファイル）1つ1つがモジュール
- .pyファイルの中の関数やクラス1つ1つもモジュール
- 前述の例では、自作のaisatsuモジュールを扱った

https://docs.python.org/ja/3/tutorial/modules.html

+++

### 標準モジュール

- Pythonの開発者が書いたプログラムでPythonと一緒に導入されるモジュール
- importして使える（自分で書いたPythonのプログラムと同じように.pyファイルがある）
- `from collections import Counter`

+++

### モジュールは配布可能

- モジュール(≒Pythonファイル)を構造化し、パッケージとして配布
- 第三者が作ったパッケージを取得し、ソースコードをPCの中に置いている
- そのため`import`ができる

+++

### パッケージの管理

- パッケージマネージャと呼ばれる管理ツールを使う
- パッケージの取得やパッケージどうしに依存関係の解決を行う

+++

### パッケージの管理に使われるコマンド

- pip（Anacondaでは極力使わない）
- conda（Anacondaでは使用を推奨）

+++

第三者が書いたパッケージの配置先



- PSFのサイトからPythonを入れた場合（※複数バージョン入れていません）
- 1箇所しかないことがのちのち問題になります

---

### 目次

- Pythonが使えるとは？
- パッケージとは？
- 環境の分離とは？
- Anacondaで環境を分離する

+++

### 1台のPCに複数プロジェクト

- 1台のPCの中で複数の開発をするもの
- ディレクトリを作ってPythonのモジュールを配置する
- このディレクトリはプロジェクトと呼ばれる

+++

### 問題：パッケージのバージョン違いが共存できない

- パッケージAについてプロジェクトXでは1系を使いたい
- プロジェクトYでは同じパッケージAの2系を使いたい
- パッケージのインストール先が1箇所だけなのが問題

+++

### おすすめの解決手段：venv

- 標準モジュールvenvを使用
- 「仮想環境を作る」
- ポイント：プロジェクトのディレクトリの下にパッケージをインストールするディレクトリが配置される
- Anaconda環境には当てはまらない

+++

### venvの仕組み 1

- `python -V`で3.7.4とします
- `cd myproject`
- `python -m venv myenv`：myprojectディレクトリの下にmyvenvができます

+++

### venvの仕組み 2

- `source myenv/bin/activate`：仮想環境を有効にします
- 仮想環境を有効にしてから`pip install`すると、パッケージは、myenv/lib/python3.7/site-packages/の下に置かれます

---

### 目次

- Pythonが使えるとは？
- パッケージとは？
- 環境の分離とは？
- Anacondaで環境を分離する

+++

### Anaconda版の「仮想環境」

- `conda create`で仮想環境を作るときは指定できる
- パッケージだけでなく、環境内のPythonのバージョンも指定できる
- 全部入りは`anaconda`を指定

+++

### 例：Anaconda版の「仮想環境」

- `conda create -n myenv python=3.7`
- myenvという名前の環境を作成
- myenvにはpython=3.7を入れる

+++

### condaコマンド注意点

condaとpipではパッケージの検索先が異なります

- pipではPyPI
- condaではAnaconda Cloud（PyPIを追加）

（condaの方がパッケージが少ない。チャネルを追加すればいい）

+++

もうちょっと書く

内容：形式が違うからどちらかにしたほうが安全

+++

AnacondaのPythonでもvenvは使えますが、科学計算のパッケージが引き継がれるわけではないので、PSFの方法でいいかなと思います。

---

### venvもNew Era

- pipenv（Anacondaと合わせて使える記載あり）
- poetry

+++

### まとめ

- 標準モジュールvenvを使った環境分離の考え方をAnacondaに導入
- 危険な方法と気づいた方は、次のプロジェクトは`conda create`して運用してみてください

+++

Special Thanks
