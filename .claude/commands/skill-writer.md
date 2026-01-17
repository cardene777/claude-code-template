---
description: パターンJSONからarticle-writerスキルのstyle/とcategories/を更新
---

skill-writerサブエージェントを起動して、以下のタスクを実行してください：

## タスク

$ARGUMENTS で提供されたパターンJSONから、article-writerスキルのテンプレートを生成してください。

## 入力データ

$ARGUMENTS

## 生成先

- @article-writer/style/format_rules.md
- @article-writer/style/wordings.md
- @article-writer/style/intro_outro.md
- @article-writer/categories/qiita/{category}.md
- @article-writer/categories/zenn/{category}.md
- @article-writer/categories/zenn-book/{category}.md

**重要**: @article-writer/templates/ は変更しない

## 期待される出力

生成完了サマリー
