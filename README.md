# TypeScript 開発環境の例
TypeScriptと、その他便利なツールを使用した環境の例です。


## 0. 使用しているツールとそのバージョン
- Node.js 15.5.0


## 1. ``npm init`` を実行
Node.jsをこのディレクトリで使用するぜー！
とりあえず ``package.json`` が生成されればいいので、何か聞かれても全部Enterでよし。


## 2. ``npm install typescript webpack webpack-cli @webpack-cli/init ts-loader -D`` を実行
``-D`` は ``--save-dev`` の略やで。TypeScriptや、webpackという、複数のJSのファイルを一つにまとめてくれる便利なツールを**開発用として**インストールしよう。これには少し時間がかかるので、ゲームでもして待とう。


## 3. ``npx webpack-cli init`` を実行
これにてwebpackの設定を行う。

### ? Will your application have multiple bundles? (お前のアプリには複数のエントリポイントがあるか?)
基本は一つだけなので、 ``n``

### ? What do you want to name your bundles? (separated by comma) (バンドル対象のファイルはどこか?)
ここではカレントディレクトリからのファイルのパスを入れるが、**拡張子は必要ない。**
``index.ts``を基本にすることが多いので、 ``src/index``

### ? In which folder do you want to store your generated bundles? (生成したバンドルファイルをどこのフォルダに入れるか?)
``dist``というフォルダにバンドルしたファイルや、コンパイルしたファイルを入れることが多いので、 ``dist``

### ? Will you use one of the below JS solutions? (どの種類のJS使っとる?)
今回はTypeScriptを使用するので、 ``typescript`` を矢印キーで選択する。

### ? Will you use one of the below CSS solutions? (どの種類のCSS使っとる?)
CSSを使用しない場合は、 ``no`` でいいが、使用する場合は ``css`` や ``sass`` などを選択する。

### ? Will you bundle your CSS files with MiniCssExtractPlugin? (CSSファイルをバンドルするとき、MiniCssExtractPlugin使う?)
CSSファイルをそのまま出力したい場合は ``y``、
``N`` にすると、バンドル時にCSSファイルの内容は、HTMLファイルの``style``タグに埋め込まれる。

### ? What will you name the CSS bundle? (CSSファイルのバンドル名は何にするん?)
バンドル元のCSSファイルの名前を入れる。
基本は ``main``

### ? Overwrite package.json? (Node.js の package.json に上書きするかい?)
既に``package.json``を生成しているので、``y``

### ? Overwrite README.md? (README.md に上書きするかい?)
既に ``README.md`` がある場合は ``y``


## 4. 生成された ``webpack.config.js`` を編集する
```JavaScript
output: {
    filename: 'bundle.js',
    path: path.join(__dirname, 'dist')
},
```
を``resolve``の下ぐらいに書き加える。
こうすることによって、バンドル時に、 ``dist`` に ``bundle.js`` が生成されるようになる。


## 5. ``npx webpack`` を実行
``src`` 内に入れてあるバンドル対象ファイルがバンドルされ、 ``dist`` に挿入される。
``npx webpack --watch`` にすると、変更するたびにバンドルされて、非常に効率的。


## 6. ``.gitignore`` を生成
Gitが管理しないファイルやフォルダを書く。
```Ignore
/dist/
/node_modules/
```
とすることによって、バンドル後のファイルと、ライブラリがたくさん入っているファイルがGit管理外になる。
(今回は``dist``は管理下にしてあるよ。)