# test-sass

npm-scripts で Sass を動かすハンズオンです。

# 1. 作業ディレクトリの作成

今回はダウンロードディレクトリに test-sass という作業ディレクトリを作成します。

```shell
cd ~/Downloads && mkdir test-sass
```

上記コマンドの翻訳は
「ダウンロードフォルダに移動したら、test-sass というフォルダを作れ」です。

# 2. Node.js のバージョンを確認

```shell
node -v
```

今回のハンズオンは 14.16.1 以上のバージョンで動作確認済みです。

# 3. package.json の作成

NPM の設定ファイル package.json を作成します。

```shell
npm init -y
```

上記コマンドの翻訳は
「すべての対話に Yes で答えて、package.json 作れ」です。

上記コマンドで作業ディレクトリのルートに package.json が作成されます。

```json
// package.json
{
{
  "name": "test-sass",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}

```

# 4. Dart Sass のインストール

```shell
npm install sass
```

開発環境ルート（ `~/Downloads/test-sass` 以降はこちらのディレクトリを開発環境ルートと呼ぶ）に node_modules というディレクトリができて、モジュール群がインストールされます。

また、 package.json が下記のように書き加えられました。

```diff
+ "dependencies": {
+   "sass": "^1.42.1"
+  }
```

dependencies というオブジェクトで依存関係を管理します。

# 5. 実際に Sass を動かしてみる　基本編

では、実際に Sass を動かしてみましょう。

開発環境ルート直下に input.scss を作成します。

```css
/* input.scss */
.test {
  &--block {
    display: flex;
    justify-content: center;
  }
}
```

実行コマンド

```css
sass --watch input.scss:output.css
```

基本形はこちらになります。
output.css と output.css.map が生成されます。

```css
/* output.css */
.test--block {
  display: flex;
  justify-content: center;
}

/*# sourceMappingURL=output.css.map */
```

CSS の整形がいつもみている形と違うかもしれません。
いつものフォーマットで整形する場合は `--style=expanded` をつけます。

一度、sass watch を `control + C` で止め、下記コマンドを実行します。

```
sass --style=expanded --watch input.scss:output.css
```

input.scss を保存すると下記ファイルが生成されます。

```css
/* output.css */
.test--block {
  display: flex;
  justify-content: center;
}

/*# sourceMappingURL=output.css.map */
```

いつものフォーマットですね。

# 6. 実際に Sass を動かしてみる　応用編 1

ディレクトリ構造を想定した場合はどのように指定すれば良いのでしょうか。

```
.
├── src
│   └── input.scss
└── styles
    └── output.css
```

## Sass ファイルの作成

作業フォルダに `src` というフォルダを作って `input.scss` というファイルを作ります。

## コンパイル

```
sass --style=expanded --watch src/input.scss:styles/output.css
```

上記コマンドを実行すると作業フォルダに `styles` というフォルダが作られて、中に `output.css` というフィいるが作られました。
