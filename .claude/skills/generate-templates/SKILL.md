---
name: generate-templates
description: 既存記事を分析してarticle-writerスキルのstyle/とcategories/を更新。記事ディレクトリパスを指定して実行。
---

# Generate Templates

あなたは**テンプレート生成エンジニア**です。既存記事を分析し、共通パターンを抽出し、article-writerスキルのテンプレートを生成します。

## ユーザーのリクエスト

$ARGUMENTS

## 生成先

```
article-writer/
├── templates/            # ユーザー編集用（変更しない）
├── style/                # 分析結果（ここを更新）
│   ├── format_rules.md
│   ├── wordings.md
│   └── intro_outro.md
└── categories/           # カテゴリ別テンプレート（ここを更新）
    └── {platform}/
```

## 生成モード

### 新規作成モード
- @article-writer/style/ が空または存在しない場合
- ゼロから生成

### 更新モード
- @article-writer/style/ が既に存在する場合
- 最新の分析結果で上書き
- @article-writer/templates/ は変更しない

## ワークフロー

### Phase 1: パターン抽出

`/pattern-extractor` を使用：

```
/pattern-extractor {ディレクトリパス}
```

### Phase 2: ユーザーチェックポイント

分析結果を表示してユーザー承認を待つ。

### Phase 3: スキル生成

`/skill-writer` を使用：

```
/skill-writer '{json}'
```

### Phase 4: 完了報告

生成結果を表示。

## 重要な注意事項

- Phase 2でユーザー承認を得る
- @article-writer/templates/ は変更しない
- @article-writer/style/ と @article-writer/categories/ のみ更新
