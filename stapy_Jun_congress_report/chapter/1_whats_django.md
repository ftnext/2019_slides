### Django Congress 2019 レポート

1. **Djangoって、何よ**
2. Django Congressレポート
3. Djangoを学ぶには？

+++

### Web開発の経験ある方🙋‍

- Pythonで
- 他の言語で
- まだ経験無し

+++

### そもそもWebアプリとは

- ブラウザ（Chrome, Firefox, Safari, etc.）から使うアプリケーション
- 今回のstapyに申し込んだ＝connpassというWebアプリを利用した

このトークではWebアプリの例としてconnpassを挙げます。

（tokibitoさん資料わかりやすい）

+++

### Webアプリを使う中で感じませんか？

- connpassにこんな機能あったらいいのに
- IT勉強会以外にも使えるconnpassみたいなアプリがあったらいいのに

→では作ってみましょう

+++

### WebアプリをPythonで作る

- Webアプリ用のパッケージ（＝**フレームワーク**）を使う
- フレームワークでは、**ルール** に則ってPythonのコードを書く
- フレームワークのルールを覚える必要あり

+++

### PythonのWebアプリフレームワーク

- **Django** 今回取り上げます
- Flask
- Falcon（ref:[2019/04stapy shimakaze_soft](https://speakerdeck.com/shimakaze01/flasktodjangoyi-wai-falseapikai-fa-falsexuan-ze-zhi)）
- etc. (FastAPI, ...)

+++

### Djangoのルール（の一部）

- URL設定
- モデル
- ビュー
- テンプレート

+++

### Webアプリにおける入出力

- 入力：リクエスト≒URLとHTTPメソッド(GET,POST,etc.)
- 出力：レスポンス≒HTML
  - Webアプリはリクエストに応じたレスポンスを返すことができます
  - 例：connpassではログインした **あなた** がstapyに申込み

+++

### Djangoがリクエストを受けてからレスポンスを返すまで

![Webアプリの動作の流れ：リクエスト→URL設定→ビュー→モデル→ビュー→テンプレート→レスポンス](elv_Feb_django_developcompass/assets/part0/django_structure.001.png)

+++

### Djangoは広大

- Webアプリに必要な機能（ログインなど）は一通り揃っている
- ゆえに広大
- Djangoだけを扱った勉強会→Django Congress
