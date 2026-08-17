# チームチャットアプリ 開発用リポジトリ

Tutorial 16「総仕上げ」で、**あなたが一本のアプリを作り切る**ための出発点です。

## 入っているもの

| | 中身 |
|:--|:--|
| `docs/spec.md` | **仕様書**。クライアントからの要求を文章にしたもの |
| `mockup/` | **画面見本**。`index.html` をブラウザで開くと全10画面を見られます |
| `docs/design/` | **設計書一式の置き場**。いまは空です。ここにあなたが設計を作ります（構成は `docs/design/README.md`） |
| Laravel と Sail | 素のLaravelと、Dockerで動かすための設定 |

## 入っていないもの

**アプリの機能のコードは、1行も入っていません。**画面もテーブルも、これから設計して、AIと一緒に作ります。

---

## 使いはじめる

1. GitHubのこのページで「**Use this template**」→「Create a new repository」から、**自分のリポジトリ**を作ります
2. 作ったリポジトリを `~/laravel-practice/` の下に clone します

```bash
cd ~/laravel-practice
git clone <自分のリポジトリのURL> teamchat-app
cd teamchat-app
```

---

## 初回起動（5手）

> ⚠️ **先に、動かしっぱなしの別アプリを止めてください。**`post-app-practice` などが起動したままだと、80番ポートと3306番ポートがぶつかって `sail up` が落ちます。そのフォルダで `./vendor/bin/sail stop` を実行してから、こちらを起動してください。

**1. ライブラリを取ってくる**

```bash
docker run --rm \
    -u "$(id -u):$(id -g)" \
    -v "$(pwd):/var/www/html" \
    -w /var/www/html \
    -e COMPOSER_CACHE_DIR=/tmp/composer_cache \
    laravelsail/php82-composer:latest \
    composer install
```

**2. 環境変数のファイルを作る**

```bash
cp .env.example .env
```

**3. コンテナを起動する**

```bash
./vendor/bin/sail up -d
```

**4. アプリケーションキーを作る**

```bash
./vendor/bin/sail artisan key:generate
```

**5. テーブルを作る**

```bash
./vendor/bin/sail artisan migrate
```

ブラウザで <http://localhost> を開いて、Laravelの初期画面が出れば準備完了です。

> 💡 5手目に `--seed` は付けません。初期データは、これから機能を作りながら自分で積んでいきます。

---

## フォルダの歩き方

```
teamchat-app/
├── docs/
│   ├── spec.md          仕様書（変えない。疑問は確認事項へ）
│   └── design/          設計書一式（あなたが作る）
├── mockup/
│   └── index.html       ここから全10画面を見る
└── （素のLaravel一式）
```

まず `mockup/index.html` をブラウザで開いて、どんなアプリを作るのかを目で見てから、`docs/spec.md` を読んでください。
