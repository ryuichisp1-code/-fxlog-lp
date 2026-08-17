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

## OGP画像について(未解決事項)

`assets/og-image.png`(1200×630)はラスター画像を生成するツールが手元に
無いため未作成。代わりに`assets/og-image.svg`を作成済み。公開前に以下の
いずれかの方法でSVGからPNGへ変換すること。

- ブラウザで`assets/og-image.svg`を開き、開発者ツールのスクリーンショット
  機能で1200×630のPNGを書き出す
- Inkscape / resvg 等のローカルツールで変換する
  (`resvg assets/og-image.svg assets/og-image.png --width 1200 --height 630`)
- オンラインのSVG→PNG変換サービスを利用する

同様に、`assets/favicon.ico`・`favicon-16.png`・`favicon-32.png`・
`favicon-192.png`・`apple-touch-icon.png`もラスター画像のため未作成。
`assets/favicon.svg`を元に、[realfavicongenerator.net](https://realfavicongenerator.net/)
等のファビコン生成サービスで一式を書き出すことを推奨する。
