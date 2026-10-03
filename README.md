# 沖縄マニア 公式サイト ― 編集ガイド

HTML・CSS・JavaScriptだけで作ったシンプルな静的サイトです。

## 公開情報

- 公開URL：https://palmawork2025-cmyk.github.io/okinawa-mania/
- SHOP：https://okinawamania.official.ec/
- Instagram：https://www.instagram.com/okinawamania.shop/

GitHub Pages で公開しています（リポジトリ：palmawork2025-cmyk/okinawa-mania）。ファイルを更新して push すると、1〜2分でサイトに反映されます。

## フォルダ構成

```
okinawa-mania/
├─ index.html        … サイト本体（文章・デザイン・動きをすべて含む）
├─ favicon.ico       … ブラウザのタブに表示されるアイコン
├─ robots.txt / sitemap.xml … 検索エンジン向けの設定
└─ images/
   ├─ okinawa-mania-logo.webp / .png    … ロゴ（OKINAWA SELECT入り・背景透過）
   ├─ okinawa-mania-logo-wordmark.webp  … ヘッダー用ロゴ
   ├─ okinawa-mania-hero.webp / -hero-sp.webp … ファーストビュー（PC用 / スマホ用）
   ├─ okinawa-mania-about.webp（＋ -800 版）  … ABOUT
   ├─ okinawa-found-item-01〜06.webp（＋ -480 版）… 発掘品カード
   ├─ okinawa-found-sign / package / arcade / blocks.webp（＋ -480 版）… 沖縄で見つけたもの / Instagram欄
   ├─ okinawa-mania-ogp.jpg  … SNSでシェアされたときの画像（1200×630）
   └─ favicon-32.png / apple-touch-icon.png / icon-512.png … アイコン（ロゴの「沖」）
```

## 表記ルール

- サイト上では販売プラットフォーム名は使わず、「SHOP」「購入はこちら」と表記します。

## URLを変更するとき

### SHOP と Instagram の URL
`index.html` の一番下にある **SITE_CONFIG** を書き換えると、サイト内のすべてのボタンに反映されます。

```js
const SITE_CONFIG = {
  shopUrl: 'https://okinawamania.official.ec/',
  instagramUrl: 'https://www.instagram.com/okinawamania.shop/',
};
```

### サイトの公開URL（独自ドメインに移すとき）
`index.html`・`robots.txt`・`sitemap.xml` の `https://palmawork2025-cmyk.github.io/okinawa-mania/` を新しいURLに一括置換します（SNSシェア画像・検索エンジン用）。

## 発掘品（商品）の差し替え

今は世界観を伝える **イメージイラスト** が入っています。実際の商品が決まったら差し替えます。

1. 商品写真を `images/` に入れます（例：`item-tin-can.webp`、横幅800px程度の正方形がおすすめ）
2. `index.html` の「▼ 発掘品カード」の `<article>` を編集します
   - `src` と `srcset` … 画像のファイル名
   - `alt` … 画像の説明（例：「沖縄で見つけたレトロな缶」）
   - `item-name` … 商品名 / `item-desc` … ひとこと説明
   - `<span class="item-tag">イメージ</span>` … 実物の写真にしたら削除
   - リンクを個別の商品ページにする場合は、`href` を変更し **`data-link="shop"` を削除**
3. 商品を増やすときは `<article>`〜`</article>` をコピーし、減らすときは削除します（3〜6点がおすすめ）
4. 実物の写真に差し替えたら、見出し下の「※現在の画像は…イメージイラストです」の注意書きも削除・変更します

> 実在しない商品名や価格は載せないでください。価格・在庫はSHOP側で管理します。

## よくある変更

| 変えたいもの | 場所 |
|---|---|
| キャッチコピー | `index.html` の `hero-copy`（＋ `<title>`、`og:title`） |
| ABOUTの文章 | `<!-- 2. 沖縄マニアについて -->` の下 |
| 「沖縄で見つけたもの」 | `<!-- 4. 沖縄で見つけたもの -->` の `found-card` |
| Instagram欄の画像 | `<!-- 5. Instagram -->` の `insta-grid` |
| ショップ情報 | `<!-- 7. SHOP INFO -->` の `info-list` |
| 色 | `<style>` の最初にある `:root { --green: … }` |

## 画像を差し替えるときのコツ

- 形式は **WebP**（無料ツール「Squoosh」などで変換できます）。ファイル名は内容がわかる英語にします
- 目安サイズ：ファーストビュー 1600×1200、商品 800×800、縦長写真 800×1000
- 写真は少し色褪せたトーン（フィルム風）にそろえると、サイト全体の統一感が保たれます
- `alt` には必ず画像の内容を書いてください（SEO・アクセシビリティのため）

## 素材の作り直し（上級者向け）

生成スクリプトは `github/okinawa-mania-tools/` にあります。
`node render.mjs`（イラスト）／`node logo.mjs`（ロゴ・favicon）／`node ogp.mjs`（OGP画像）
