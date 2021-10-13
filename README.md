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
{
  "name": "test-sass",
  "version": "1.0.0",
  "description": "npm-scripts で SASS を動かすハンズオンです。",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/YoshinoriKanno/test-sass.git"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/YoshinoriKanno/test-sass/issues"
  },
  "homepage": "https://github.com/YoshinoriKanno/test-sass#readme"
}
```

# 4. Dart Sass のインストール

```shell
npm install sass
```

ルートに node_modules というディレクトリができて、モジュール群がインストールされます。

また、 package.json が下記のように書き換えられました。

```diff
-  "homepage": "https://github.com/YoshinoriKanno/test-sass-2#readme"
+  "homepage": "https://github.com/YoshinoriKanno/test-sass-2#readme",
+  "dependencies": {
+    "sass": "^1.42.1"
+  }

```

dependencies というオブジェクトで依存関係を管理します。
