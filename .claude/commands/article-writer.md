---
name: article-writer
description: アウトラインとwriting-styleに従って記事を執筆
---

article-writerサブエージェントを起動して、以下のタスクを実行してください：

## タスク

$ARGUMENTS で提供されたアウトラインとwriting-styleに従って、高品質な技術記事を執筆してください。

## 入力データ

$ARGUMENTS

形式:
```json
{
  "outline": {
    "platform": "zenn-article",
    "category": "technical-tutorial",
    "title": "記事タイトル",
    "sections": [...]
  },
  "analysis": {
    "theme": {...},
    "problem": {...},
    "solution": {...}
  }
}
```

## 執筆要件

1. **writing-styleスキルをロード**
2. **generated/のルールを優先的に参照**
3. **セクションごとに執筆**:
   - はじめに（intro_outro.mdのテンプレート使用）
   - 本文セクション（format_rules.md、wordings.md準拠）
   - コード例の挿入
   - 最後に（intro_outro.mdのテンプレート使用）
4. **内部品質チェックを実施**
5. **完成記事をMarkdown形式で返す**

## 期待される出力

完成したMarkdown記事（frontmatter付き）:

```markdown
---
title: "記事タイトル"
emoji: "📝"
type: "tech"
topics: ["tag1", "tag2"]
published: true
---

## はじめに

[intro_outro.mdのテンプレートに従った内容]

## セクション1

[format_rules.mdとwordings.mdに従った内容]

...

## 最後に

[intro_outro.mdのテンプレートに従った内容]
```

## 重要な制約

- writing-styleスキルを必ずロードする
- generated/を優先的に参照（ユーザー固有のスタイル）
- 内部品質チェックを必ず実施
- 完成記事のみを返す（途中経過は返さない）
- ローカルファイルパス（`.claude/`, `/Users/`）を含まない
