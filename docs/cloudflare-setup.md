# Cloudflare Pages セットアップ手順

FXログ LP(`fxlog-lp`リポジトリ)をCloudflare Pagesで公開するための手順書。
Cloudflareアカウントは作成済みの前提で進める。

## 1. Cloudflareにログイン

1. https://dash.cloudflare.com にアクセスし、ログインする。

## 2. Pagesプロジェクトを作成する

1. 左サイドバーの **Workers & Pages** をクリック。
2. **Create application** ボタンをクリック。
3. 上部タブで **Pages** を選択。
4. **Connect to Git** をクリック。
5. GitHubアカウントとの連携がまだの場合は、画面の指示に従って
   Cloudflare ↔ GitHub の連携(OAuth認可)を行う。
6. リポジトリ一覧から **`fxlog-lp`** を選択し、**Begin setup** をクリック。

## 3. ビルド設定

以下の内容で設定する(静的HTML/CSSのみのプロジェクトのため、ビルドコマンドは不要):

| 項目 | 設定値 |
|---|---|
| Project name | `fxlog-lp`(任意、後で`*.pages.dev`のサブドメインになる) |
| Production branch | `main` |
| Framework preset | `None` |
| Build command | (空欄のまま) |
| Build output directory | `/` |

設定後、**Save and Deploy** をクリックする。

## 4. 環境変数

現時点では環境変数は不要(空欄のまま進めてよい)。

Cloudflare Web Analytics導入時(Phase 6-3 Step 8で対応予定)に、必要であれば
このタイミングで追加の環境変数設定に戻ってくる。

## 5. デプロイ完了確認

1. 初回デプロイが完了すると、`https://fxlog-lp.pages.dev`
   (プロジェクト名が異なる場合はそれに応じたURL)のようなサブドメインが
   発行される。
2. このURLにアクセスし、Coming Soonページが正しく表示されることを確認する。

## 6. カスタムドメインを追加する(fxlog.link-ai17.jp)

FXログLPは**サブドメイン運用**(`fxlog.link-ai17.jp`)とする。apex
(`link-ai17.jp`)は将来別用途に使う可能性を残すため、本プロジェクトからは
一切設定しない。

1. 作成したPagesプロジェクトの管理画面を開く。
2. **Custom domains** タブをクリック。
3. **Set up a custom domain** をクリック。
4. `fxlog.link-ai17.jp` と入力し、**Continue** をクリック。
5. 画面に **Cloudflareが指定するDNSレコードの内容**(通常はCNAME、
   `<プロジェクト名>.pages.dev`宛)が表示されるので、必ずメモしておく。
   → この内容を次の `docs/xserver-dns-setup.md` の手順で
     Xサーバー側のDNS設定に反映する。
6. DNS側の設定が反映されると、Cloudflareが自動的にSSL証明書(Let's Encrypt
   または Google Trust Services)を発行する。反映には数分〜数時間かかる
   場合がある。

## 7. 動作確認

1. `https://fxlog.link-ai17.jp` にHTTPSでアクセスできることを確認する。
2. ブラウザの鍵アイコンからSSL証明書が有効であることを確認する。
3. apex(`https://link-ai17.jp`)は本プロジェクトの対象外のため、本手順
   では触れない・確認もしない。

## 8. 以降のデプロイ運用

`main`ブランチへのpushをトリガーに、Cloudflare Pagesが自動的に再ビルド・
再デプロイを行う。手動デプロイ操作は不要。

---

## 参考: この手順が前提とするリポジトリ構成

```
fxlog-lp/
├── index.html
├── styles/main.css
├── assets/
├── _headers
├── _redirects
├── robots.txt
└── sitemap.xml
```

`_headers`・`_redirects`はCloudflare Pages独自の設定ファイルで、リポジトリ
ルート(Build output directoryの直下)に置くだけで自動的に読み込まれる。
