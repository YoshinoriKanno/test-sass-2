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

下記のようにディレクトリ構造を想定した場合はどのように指定すれば良いのでしょうか。

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

# 7. 実際に Sass を動かしてみる　応用編 2

では、下記のようなディレクトリ構造を想定した場合はどのように指定すれば良いのでしょうか。
みなさんが、通常プロジェクトや特集などで使っている出るフォルダ構成に近い形です。

```
.
├── src
│   ├── main.scss
│   └── _export.scss
└── styles
    └── main.css
```

## Sass ファイルの作成

作業フォルダに `src` というフォルダを作って `main.scss` と `_export.scss` というファイルを作ります。

```css
// input.scss
@import "export";

.test {
  &--block {
    display: flex;
    justify-content: center;
  }
}
```

```css
// _export.scss
.export {
  text-align: center;
}
```

## コンパイル

```shell
sass --style=expanded --watch src:styles
```

上記コマンドを実行すると作業フォルダに `styles` というフォルダが作られて、中に `main.css` というフィいるが作られました。

# 8. autoprefixer の実行

autoprefixer は Can I Use の値を使って CSS を解析し、CSS ルールにベンダープレフィックスを追加する PostCSS プラグインです。

## インストール

下記コマンドで autoprefixer をインストールします。

```shell
npm install postcss postcss-cli autoprefixer
```

autoprefixer を npm Scripts で使う場合、postcss, postcss-cli に依存関係があるので postcss, postcss-cli も一緒にインストールしています。

実行すると各種パッケージがダウンロードされて package.json が書き換えれます。

```diff
+  "autoprefixer": "^10.3.7",
+  "postcss": "^8.3.9",
+  "postcss-cli": "^9.0.1",
```

## package.json にブラウザリストを追記する

```diff
+   "browserslist": [
+     "last 2 versions",
+     "ie >= 11",
+     "Android >= 4"
+   ]
```

## autoprefixer を実行する

実行コマンドはこちらです。

```shell
npx postcss styles/**/*.css --use autoprefixer --replace
```

```css
// styles/main.css
.export {
  text-align: center;
}

.test--block {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: center;
  -ms-flex-pack: center;
  justify-content: center;
}

/*# sourceMappingURL=data:application/json;base64,eyJ2ZXJzaW9uIjozLCJzb3VyY2VzIjpbIi4uL3NyYy9fZXhwb3J0LnNjc3MiLCJtYWluLmNzcyIsIi4uL3NyYy9tYWluLnNjc3MiXSwibmFtZXMiOltdLCJtYXBwaW5ncyI6IkFBQ0E7RUFDRSxrQkFBa0I7QUNBcEI7O0FDRUU7RUFDRSxvQkFBYTtFQUFiLG9CQUFhO0VBQWIsYUFBYTtFQUNiLHdCQUF1QjtNQUF2QixxQkFBdUI7VUFBdkIsdUJBQXVCO0FEQzNCIiwiZmlsZSI6Im1haW4uY3NzIn0= */
```

autoprefixer をかける前

```css
.export {
  text-align: center;
}

.test--block {
  display: flex;
  justify-content: center;
}

/*# sourceMappingURL=main.css.map */
```

map が不要な場合は --no-map オプションをつけます。

```
npx postcss styles/**/*.css --use autoprefixer --replace --no-map
```
