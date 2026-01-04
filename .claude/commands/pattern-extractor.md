---
name: pattern-extractor
description: 既存記事を分析してパターンをJSON形式で抽出
---

pattern-extractorサブエージェントを起動して、以下のタスクを実行してください：

## タスク

$ARGUMENTS で指定されたディレクトリパス内の記事を分析し、カテゴリ・構造・トーン・コードパターンをJSON形式で抽出してください。

## 分析対象

ディレクトリパス: $ARGUMENTS

例: `qiita/articles/, zenn/articles/`

## 期待される出力

以下のJSON形式で結果を返してください：

```json
{
  "total_articles": <number>,
  "platforms": {
    "qiita": {
      "count": <number>,
      "categories": [
        {
          "name": "カテゴリA",
          "count": <number>,
          "percentage": <number>,
          "structure_pattern": ["セクション1", "セクション2"],
          "example_articles": ["article1.md"]
        }
      ]
    }
  },
  "tone_patterns": {...},
  "code_patterns": {...}
}
```

## 重要な制約

- すべての記事を全文読み込む（導入部だけではなく）
- カテゴリ分類はコンテンツベースで行う
- 推測を避け、実際のデータに基づいて分析する
- 結果はJSON形式のみで返す（mainのコンテキストを圧迫しない）
