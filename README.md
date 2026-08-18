# FXログ LP - Public Website

FXログ(4象限で振り返るFXトレード記録アプリ)の公式サイト。

## 概要

- 公開URL: https://fxlog.link-ai17.jp
- ホスティング: Cloudflare Pages
- ドメイン管理: Xサーバー
- アーキテクチャ: 静的HTML/CSS
- 分析: Cloudflare Web Analytics(Step 8で導入予定)

## 現在のステータス

- [x] Step 1-3: プロジェクト初期化 + Coming Soonページ
- [ ] Step 4: ヒーローセクション + セールスレター
- [ ] Step 5: 機能紹介(四象限分析 + SNS共有)
- [ ] Step 6: 価格プラン + 特定商取引法
- [ ] Step 7: FAQ + フッター + SEO/OGP
- [ ] Step 8: Cloudflare Web Analytics導入
- [ ] Step 9: 最終調整 + Lighthouse
- [ ] Step 10: 本公開差替え

## 開発

ローカル確認: `index.html`をブラウザで直接開く、またはPythonで簡易サーバーを起動する。

```bash
python -m http.server 8000
# http://localhost:8000 にアクセス
```

## デプロイ

`main`ブランチへのpushでCloudflare Pagesが自動デプロイする。

## セットアップ手順

- [docs/cloudflare-setup.md](docs/cloudflare-setup.md) — Cloudflare Pagesプロジェクト作成〜カスタムドメイン設定
- [docs/xserver-dns-setup.md](docs/xserver-dns-setup.md) — Xサーバー側のDNSレコード設定

## v1.1リリース予定日

2026-08-31

## OGP画像・favicon(ラスター画像)について

`assets/`配下のSVGソースとPNG/ICO生成物の役割分担は以下の通り。

- `assets/og-image.svg` — **ブラウザ表示用**(filterあり、`feDropShadow`による
  ゴールドセルのglowエフェクト付き)
- `assets/og-image-flat.svg` — **PNG変換用**(filterなし、SVGコンバーター互換版)。
  CloudConvertがfeDropShadow(filter要素)を処理できず、左上セルのゴールド
  塗りつぶしごと消える不具合が確認されたため分離した
- `assets/og-image.png`(1200×630) — `og-image-flat.svg`から生成した最終成果物。
  OGP/Twitter Cardタグから参照される

### PNG変換手順(og-image.png再生成が必要な場合)

1. https://cloudconvert.com/svg-to-png にアクセス
2. `assets/og-image-flat.svg` をアップロード
3. Options → Width: `1200`, Height: `630` を指定
4. Convert → Download
5. ダウンロードしたファイルを `og-image.png` として `assets/` に配置(上書き)

### favicon一式について

`assets/favicon.svg`(モダンブラウザ優先)に加え、`favicon.ico`・
`favicon-96.png`・`favicon-192.png`・`apple-touch-icon.png`(180×180)を
[realfavicongenerator.net](https://realfavicongenerator.net/)で生成し配置済み
(16×16/32×32は同ツールが生成しなかったため96×96/192×192の2サイズで代替)。
