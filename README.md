# Re:View技術書執筆環境（Docker版）

Docker ComposeとVS Code Dev Containerを使ったRe:View執筆環境です。
TechBoosterのRe:VIEWテンプレートを使用して、技術書向けのスタイル設定が適用されています。

## 環境構成

```
your-book-project/
├── .devcontainer/
│   └── devcontainer.json
├── docker-compose.yml
├── articles/
│   └── techbook_0_sample/    # TechBoosterテンプレート
│       ├── *.re              # 原稿ファイル
│       ├── config.yml        # 書籍設定
│       ├── catalog.yml       # 章構成
│       ├── Rakefile          # ビルドタスク
│       ├── sty/              # LaTeXスタイル
│       └── images/           # 画像ファイル
└── README.md
```

## 使い方

### 環境の起動

```bash
# VS Codeで開く
code .

# コマンドパレット (Cmd/Ctrl+Shift+P) で
# "Dev Containers: Reopen in Container" を実行
```

### PDFの生成

```bash
cd articles/techbook_0_sample
rake pdf
```

#### 電子版

```bash
REVIEW_CONFIG_FILE=config-ebook.yml rake pdf
```

### 新しいプロジェクトの作成

```bash
# techbook_0_sampleディレクトリを丸ごとコピー
cd articles
cp -r techbook_0_sample techbook_1_newproject

# 新しいプロジェクトに移動
cd techbook_1_newproject

# config.ymlを編集して書籍情報を更新
# booktitle, aut, date などを変更

# PDFをビルド
rake pdf
```

## その他のビルドコマンド

```bash
# EPUB作成
rake epub

# HTML作成
rake web

# テキスト形式で出力
rake text

# 全形式でビルド
rake all
```

## 設定ファイル

- `config.yml`: 書籍のメタ情報（タイトル、著者、日付など）
- `catalog.yml`: 章の構成と順序
- `sty/`: LaTeXのスタイルファイル（PDF出力のデザイン）
- `style.css`: HTML/EPUB用のスタイル

## テンプレートについて

このプロジェクトでは[TechBoosterのRe:VIEWテンプレート](https://github.com/TechBooster/ReVIEW-Template)を使用しています。
技術書向けに最適化されたスタイル設定が含まれています。

## 文章校正（textlint）

このプロジェクトには日本語技術文書向けのtextlintが導入されています。

### 校正の実行

```bash
# 全ての.reファイルをチェック
npm run textlint

# 自動修正可能な問題を修正
npm run textlint:fix

# ドライラン（実際には修正しない）
npm run textlint:check
```

設定は`.textlintrc.json`で変更できます。

## トラブルシューティング

### PDFビルドでエラーが出る場合

```bash
# クリーンビルド
rake clean
rake pdf
```

### 日本語フォントの問題

Docker環境には日本語フォントが含まれているため、特別な設定は不要です。

## 参考リンク

- [Re:VIEW公式ドキュメント](https://reviewml.org/)
- [TechBooster/ReVIEW-Template](https://github.com/TechBooster/ReVIEW-Template)
- [Re:VIEW記法ガイド](https://github.com/kmuto/review/blob/master/doc/format.ja.md)
