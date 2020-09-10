---
title: Cypress のインストール
---

{% note info %}
# {% fa fa-graduation-cap %} 学習すること

- How to install Cypress via `npm`
- Cypress を `npm` を使用してインストールする方法
- Cypress を直接ダウンロードしてインストールする方法
- `package.json` を使用した Cypress のバージョン管理および実行する方法

{% endnote %}

# システム要件

### OS

Cypress はインストールして使用するデスクトップアプリケーションです。Cypress は以下の OS をサーポートしています:

- **MacOS** 10.9 以上 *(64-bit のみ)*
- **Linux** Ubuntu 12.04 以上、Fedora 21、Debian 8 *(64-bit のみ)*
- **Windows** 7 以上

### Node.js

`npm` を使用して Cypress をインストールする場合:

- **Node.js** 10 または 12 以上

### Linux

Linux を使用する場合、以下のソフトウェアがインストールされている必要があります。

必要なソフトウェアが全てインストールされた、公式の Docker コンテナ {% url 'cypress/base' 'https://hub.docker.com/r/cypress/base/' %} もあります。

{% partial linux_dependencies %}

# インストール方法

## {% fa fa-terminal %} `npm install`

Cypress を `npm` を使用してインストールします:

```shell
cd /your/project/path
```

```shell
npm install cypress --save-dev
```

これでプロジェクトに開発時の依存関係として Cypress がインストールされます。

{% note info %}
Cypress を正しいフォルダーにインスールするため、事前に {% url "`npm init`" https://docs.npmjs.com/cli/init %} が実行されていること、`node_modules` が存在すること、プロジェクトのルートフォルダーに `package.json` があることを確認してください。
{% endnote %}

{% video local /img/snippets/installing-cli.mp4 %}

{% note info %}
Cypress の `npm` パッケージは Cypress の実行ファイルのラッパーであることに気を付けてください。`npm` のバージョンはダウンロードされる実行ファイルのバージョンを示します。バージョンが `3.0` ならば、コンピューターのグローバルキャッシュフォルダーにダウンロードされ、他のプロジェクトと共有で使用されます。
{% endnote %}

{% note success Best Practice %}

`npm` を使用して Cypress をインストールするのがおすすめです。理由は以下の通りです:

- Cypress が他の依存関係と同様にバージョン管理される
- {% url '継続的インテグレーション (CI)' continuous-integration %} での Cypress の実行を単純化させる
{% endnote %}

## {% fa fa-terminal %} `yarn add`

Cypress を {% url "`yarn`" https://yarnpkg.com %} を使用してインストールします:

```shell
cd /your/project/path
```

```shell
yarn add cypress --dev
```

## {% fa fa-download %} 直接ダウンロードする

Node や `npm` をプロジェクトで使用していない場合や、Cypress をすぐに試してみたい場合は、いつでも {% url "Cypress を CDN からダウンロードできます" https://download.cypress.io/desktop %}。

{% note warning %}
直接ダウンロードした場合は、ダッシュボードに録画することが出来ません。ダウンロードは Cypress をすぐに実行してもらうために用意しています。ダッシュボードにテストを録画する際は、Cypress を `npm` の依存関係としてインストール必要があります。
{% endnote %}

直接ダウンロードする場合は常に最新バージョンとなります。実行するプラットフォームは自動的に選択されます。

ダウンロードされたファイルを解凍し、実行します。Cypress は依存関係なく実行されます。

{% video local /img/snippets/installing-global.mp4 %}

## {% fa fa-refresh %} CI

CI 環境に Cypress を導入するには{% url '継続的インテグレーション' continuous-integration %}を参照してください。Linux で実行する場合にはいくつか{% url '依存関係' continuous-integration#Dependencies %}を解決する必要がありますが、事前に設定済みの {% url 'Docker イメージ' docker %}を使用することもできます。

# Cypress を起動する

Cypress のインストールに `npm` を使用している場合、Cypress はプロジェクトの `./node_modules` フォルダーにインストールされ、インストールされた実行ファイルは `./node_modules/.bin` から実行できます。

**プロジェクトルート**フォルダーから Cypress を起動するには以下の方法があります:

**フルパスを指定する**

```shell
./node_modules/.bin/cypress open
```

**もしくは、ショートカットとして `npm bin` を使用する**

```shell
$(npm bin)/cypress open
```

**もしくは、`npx` を使用する**

**注意**: {% url "npx" https://www.npmjs.com/package/npx %} は `npm > v5.2` に含まれていますし、個別にインストールすることもできます。

```shell
npx cypress open
```

**もしくは、`yarn` を使用する**

```shell
yarn run cypress open
```

しばらくすると、Cypress テストランナーが起動します。

## ブラウザーを切り替える

Cypress テストランナーはユーザーのコンピューターにあるブラウザーを全て見つけようと試みます。ブラウザーを切り替えるためのドロップダウンリストがテストランナーの右上部にあります。

{% imgTag /img/guides/browser-list-dropdown.png "ブラウザーを切り替える" %}

end-to-end テストを実行する際に Cypress がどのようにブラウザーを制御するかについては、{% url "ブラウザーを起動する" launching-browsers %}を参照してください。

{% note info Cross Browser Support %}

Cypress は現在 Firefox と Chrome 系のブラウザー (Edge や Electron を含みます) をサポートしています。CI 環境でこれらのブラウザーのテストを最適化したい場合は、{% url "クロスブラウザーのテストガイド" cross-browser-testing %}に実例があるので確認してみてください。

{% endnote %}

## npm スクリプトを追加する

Cypress への実行パスを毎回書いてもなんら問題はないのですが、`package.json` ファイルの `scripts` フィールドに Cypress コマンドを追加する方がわかりやすくて簡単です。

```javascript
{
  "scripts": {
    "cypress:open": "cypress open"
  }
}
```

これで、プロジェクトルートからこのように実行できます:

```shell
npm run cypress:open
```

...これで Cypress が起動します。

# CLI ツール

`npm` を使用して Cypress をインストールすることで、その他の CLI コマンドが使用できるようになります。

Cypress のバージョン `0.20.0` では、`node_module` に Node スクリプトに必要なファイルが構築されます。

{% url 'CLI ツールに関してはこちら' command-line %}を参照してください。

# 上級者向け

## 環境変数

名前 | 説明
------ |  ---------
`CYPRESS_INSTALL_BINARY` | {% urlHash "Cypress の実行ファイルがダウンロードされ、インストールされる場所" Install-binary %}
`CYPRESS_DOWNLOAD_MIRROR` | {% urlHash "ミラーサーバーから Cypress をダウンロードする"  Mirroring %}
`CYPRESS_CACHE_FOLDER` | {% urlHash "Cypress の実行ファイルのキャッシュが配置される場所" Binary-cache %}
`CYPRESS_RUN_BINARY` | {% urlHash "Cypress の実行ファイルの場所" Run-binary %}
~~CYPRESS_SKIP_BINARY_INSTALL~~ | {% badge danger removed %} 代わりに `CYPRESS_INSTALL_BINARY=0` を使用してください
~~CYPRESS_BINARY_VERSION~~ | {% badge danger removed %} 代わりに `CYPRESS_INSTALL_BINARY` を使用してください

## 実行ファイルのインストール

環境変数 `CYPRESS_INSTALL_BINARY` を使用することで、Cypress をどのようにインストールするかを制御することができます。現在設定済みの値を上書きするには、`npm install` と一緒に指定します。

**次の場合に便利です:**

- npm で指定したバージョンと違うバージョンをインストールする。
    ```shell
CYPRESS_INSTALL_BINARY=2.0.1 npm install cypress@2.0.3
    ```
- (会社のファイアーウォールを通すために) 外部の URL を指定する。
    ```shell
CYPRESS_INSTALL_BINARY=https://company.domain.com/cypress.zip npm install cypress
    ```
- インターネットの代わりにローカルのファイルを指定してインストールする。
    ```shell
CYPRESS_INSTALL_BINARY=/local/path/to/cypress.zip npm install cypress
    ```

上記の全てのケースで、実行ファイルを所定以外の場所からインストールした事実は *`package.json` ファイルに記録されません*。同じようにインストールするためには、繰り返し同様の環境変数を指定しなければなりません。

### インストールをスキップする

`CYPRESS_INSTALL_BINARY=0` を指定することで、Cypress のアプリケーションのインストールをスキップすることができます。これは `npm install` のタイミングで Cypress をダウンロードしたくない場合に便利でしょう。

```shell
CYPRESS_INSTALL_BINARY=0 npm install
```

これで Cypress の npm モジュールがインストール済みの場合には Cypress 自体のインストールを行わなくなります。

## 実行ファイルのキャッシュ

Cypress のバージョン `3.0` では、システムのグローバルキャッシュに、該当する実行ファイルをダウンロードするので、実行ファイルはプロジェクト間で共有されます。デフォルトではグローバルキャッシュフォルダーは以下の通りです:

- **MacOS**: `~/Library/Caches/Cypress`
- **Linux**: `~/.cache/Cypress`
- **Windows**: `/AppData/Local/Cypress/Cache`

デフォルトのキャッシュフォルダーを上書きするには、環境変数 `CYPRESS_CACHE_FOLDER` を設定します。

```shell
CYPRESS_CACHE_FOLDER=~/Desktop/cypress_cache npm install
```

```shell
CYPRESS_CACHE_FOLDER=~/Desktop/cypress_cache npm run test
```

Cypress は自動的に `~` をユーザーのホームフォルダーに置き換えます。なので、CI 環境の設定ファイルで `CYPRESS_CACHE_FOLDER` は次のように書くことが出来ます:

```yml
environment:
  CYPRESS_CACHE_FOLDER: '~/.cache/Cypress'
```

{% url '継続的インテグレーション - キャッシュ' continuous-integration#Caching %}のセクションも参照してください。

{% note warning %}
`CYPRESS_CACHE_FOLDER` は Cypress の起動時に必ず存在する必要があります。環境変数を `.bash_profile` (MacOS, Linux) や、`RegEdit` (Windows) を使用してシステムに登録してください。
{% endnote %}

## 実行する

環境変数 `CYPRESS_RUN_BINARY` を設定することで、Cypress 実行ファイルを npm モジュールが探しに行く場所を上書きすることができます。

`CYPRESS_RUN_BINARY` は解答された実行ファイルのパスでなければなりません。Cypress の `open`、`run`、`verify` コマンドがその実行ファイルを使用して起動します。

### Mac

```shell
CYPRESS_RUN_BINARY=~/Downloads/Cypress.app/Contents/MacOS/Cypress cypress run
```

### Linux

```shell
CYPRESS_RUN_BINARY=~/Downloads/Cypress/Cypress cypress run
```

### Windows

```shell
CYPRESS_RUN_BINARY=~/Downloads/Cypress/Cypress.exe cypress run
```

{% note warning %}
環境変数 `CYPRESS_RUN_BINARY` を設定することにより、システム上の Cypress モジュール全てに影響を及ぼすため、システムには**設定しないこと**をおすすめします。
{% endnote %}

## ダウンロード用の URL

特定のプラットフォーム (OS) や、特定のバージョン向けの Cypress をダウンロードする場合は CDN を使用してください。

ダウンロードサーバーの URL は `https://download.cypress.io` です。

以下のファイルがダウンロードできます:

- Windows 64-bit (`?platform=win32&arch=x64`)
- Windows 32-bit (`?platform=win32&arch=ia32`、{% url "Cypress 3.3.0" changelog#3-3-0 %} から使用可能です)
- Linux 64-bit (`?platform=linux`)
- macOS 64-bit (`?platform=darwin`)

ダウンロード用の URL はこちらです:

使用可能な全てのプラットフォームは {% url "https://download.cypress.io/desktop.json" https://download.cypress.io/desktop.json %} を参照下さい。

 メソッド | URL                            | 説明
 ------- | ------------------------------ | -------------------------------------------------------------------------
 `GET`   | `/desktop`                     | 最新バージョンの Cypress をダウンロードします (プラットフォームは自動選択)
 `GET`   | `/desktop.json`                | ダウンロード可能な最新の CDN の URL を含む JSON を返します
 `GET`   | `/desktop?platform=p&arch=a`   | 特定のプラットフォームまたはアーキテクチャーの Cypress をダウンロードします
 `GET`   | `/desktop/:version`            | 特定のバージョンの Cypress をダウンロードします
 `GET`   | `/desktop/:version?platform=p&arch=a` | 特定のバージョン、プラットフォームまたはアーキテクチャーの Cypress をダウンロードします

**64-bit 向け Windows の Cypress `3.0.0` をダウンロードする際の URL:**

```text
https://download.cypress.io/desktop/3.0.0?platform=win32&arch=x64
```

## ミラーサイト

Cypress のダウンロードをミラーサイトに切り替える場合は、`CYPRESS_DOWNLOAD_MIRROR` を指定して、ダウンロードサーバーの URL を `https://download.cypress.io` からご自身のミラーサイトに変更することができます。

例:

```shell
CYPRESS_DOWNLOAD_MIRROR="https://www.example.com" cypress install
```

Cypress は実行ファイルを次のようなフォーマットでダウンロードを試みます: `https://www.example.com/desktop/:version?platform=p`

## Cypress への例外データ送信をオプトアウトする

Cypress の問題で例外が発生した場合、例外に関するデータを `https://api.cypress.io` に送信します。この情報はより良い製品を開発するためだけに使用します。

`CYPRESS_CRASH_REPORTS=0` を環境変数に設定することで、Cypress への例外データの送信をオプトアウトすることが可能です。

### Linux または macOS でのオプトアウト

Linux または macOS で例外データ送信をオプトアウトするためには、Cypress をインストールする前にターミナルで以下のコマンドを実行してください:

```shell
export CYPRESS_CRASH_REPORTS=0
```

この変更を永続化するには、このコマンドをご使用のシェルの `~/.profile` (`~/.zsh_profile`、`~/.bash_profile` 等) に追加し、ログイン時に実行されるようにしてください。

### Windows でのオプトアウト

Windows で例外データ送信をオプトアウトするためには、Cypress をインストールする前にコマンドプロンプトで以下のコマンドを実行してください:

```shell
set CYPRESS_CRASH_REPORTS=0
```

Powershell では以下のようにしてください:

```shell
$env:CYPRESS_CRASH_REPORTS = "0"
```

環境変数 `CYPRESS_CRASH_REPORTS` を保存し、新しいシェルで使えるようにするには `setx` を使用してください:

```shell
setx CYPRESS_CRASH_REPORTS 0
```

## プレリリース版をインストールする

発行されていない {% url "`develop`" https://github.com/cypress-io/cypress/commits/develop %} ブランチの修正を確認するため、プレリリース版をインストールしたいと思っているかもしれません。

{% note info %}
プレリリース版に含まれる予定の issue は{% url "こちら" https://github.com/cypress-io/cypress/issues?utf8=%E2%9C%93&q=label%3A%22stage%3A+pending+release%22+ %}で全て確認できます。
{% endnote %}

{% url "`develop`" https://github.com/cypress-io/cypress/commits/develop %} ブランチへのコミットは各プラットフォーム向けにビルドされ、下流のプロジェクトに対してテストされます。例えば、次のイメージでは最新のコミットが `e5106d9` という SHA ハッシュを持っています。

{% imgTag /img/guides/install/last-commit.png "Last commit on develop branch" %}

The simplest way to find the pre-release version of the Test Runner matching this commit is to look at the commits made on our projects under test at {% url "cypress-test-example-repos" https://github.com/cypress-io/cypress-test-example-repos/commits/master %}. You will see individual commits for each built platform and architecture: `darwin` (Mac), `linux`, `win 32bit` and `win 64bit`. The built commit SHA `e5106d9` is in the subject line of the test commit:

{% imgTag /img/guides/install/test-commits.png "Test commit per platform" %}

These pre-release builds are platform-specific. Choose the platform that matches your platform; for example if you are on a Mac, click on the commit "Testing new darwin x64 ...". This commit has a custom message that shows a special temporary URL of the built binary for Mac OS and the matching npm `cypress` package.

{% imgTag /img/guides/install/beta-binary.png "Beta binary information" %}

To install this pre-release binary on Mac, you need to set the `CYPRESS_INSTALL_BINARY` environment variable to the shown `https://cdn.cypress.io/beta/binary/.../cypress.zip` value and run `npm install https://cdn.cypress.io/beta/npm/3.3.2/.../cypress.tgz`. The command in the terminal will be:

```shell
export CYPRESS_INSTALL_BINARY=https://cdn.cypress.io/beta/binary/3.3.2/darwin-x64/circle-develop-e5106d95f51eec477b8e66609939979fb87aab56-126014/cypress.zip
```

```shell
npm install https://cdn.cypress.io/beta/npm/3.3.2/circle-develop-e5106d95f51eec477b8e66609939979fb87aab56-126013/cypress.tgz
```

If my machine is Windows 64bit, I will click on the "Testing new win32 x64 ..." commit and run the command below.

```shell
set CYPRESS_INSTALL_BINARY=https://cdn.cypress.io/beta/binary/3.3.2/win32-x64/appveyor-develop-e5106d95f51eec477b8e66609939979fb87aab56-25451270/cypress.zip
```

```shell
npm install https://cdn.cypress.io/beta/npm/3.3.2/appveyor-develop-e5106d95f51eec477b8e66609939979fb87aab56-25451270/cypress.tgz
```

On Linux CI you should install the binary from the "Testing new linux x64 ..." commit.

```shell
export CYPRESS_INSTALL_BINARY=https://cdn.cypress.io/beta/binary/3.3.2/linux-x64/circle-develop-e5106d95f51eec477b8e66609939979fb87aab56-125973/cypress.zip
```

```shell
npm install https://cdn.cypress.io/beta/npm/3.3.2/circle-develop-e5106d95f51eec477b8e66609939979fb87aab56-125992/cypress.tgz
```

### Pre-release binary URL format

The above `CYPRESS_INSTALL_BINARY` urls are temporary - they are purged after 30 days. The format of the url is as follows:

```text
https://cdn.cypress.io/beta/binary/&lt;version&gt;/&lt;platform&gt;-&lt;arch&gt;/
&lt;ci name&gt;-&lt;branch name&gt;-&lt;full commit SHA&gt;-&lt;CI build number&gt;/cypress.zip
```
