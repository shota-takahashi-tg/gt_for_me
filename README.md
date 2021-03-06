
# gt_for_me

## :warning:以下、別のリポジトリ用の下書き:warning:

### Firebaseトークン認証 on GAE/GO 動確@0208

#### Notice

* 各技術のチュートリアルを組み合わせて流れで作ってしまったので、いろいろ構造がおかしかったりすると思います
* GAEのdev環境では、認証部分のレスポンスが 502 になってしまう現象が発生中です
  * GAEコンソール上では、想定通りのレスポンスを返していることを確認済み
  * @sinmetal様に相談したところ、GAEのフロント部分で何か起こってるかも、とのこと

#### 事前準備

* GAE/GO SDKをインストールしておく
* glideをインストールしておく
* 他、基本的な開発環境は各員で準備するものとする
	* 自分用 - https://github.com/shota-takahashi-tg/gt_for_me/wiki/%E7%92%B0%E5%A2%83%E6%A7%8B%E7%AF%89

#### ローカルで動作確認 for Mac
※一部雰囲気で書いています
```
export MYGOPATH={適当に}
cd $MYGOPATH/src
git clone {このリポジトリ}
cd static
glide install
goapp install ./...
goapp serve static/backend
```

* http://localhost:8080/firebase/auth/google-popup.html にアクセス
* GAE側のアクセス制限画面が出たら、適当なメアド + チェックボックスONでログイン
* `SIGNIN WITH GOOGLE` を押下して適当なアカウントでログイン
* 画面下部の <span style="color:red">Verified!</span> を確認

#### フォルダ・ファイル役割
* `backend/hello.go`
	* サーバーサイドプログラム
	* 認証周りは↓からコピペ
	* https://github.com/ionTea/go-GAE-firebase-verify
* `backend/firebase`
	* ブラウザクライアントでのFirebase認証部分
	* 公式ドキュメントのQuickStart用リポジトリを流用
	* https://github.com/firebase/quickstart-js
