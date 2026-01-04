---
name: skill-writer
description: パターンJSONからarticle-templatesとwriting-styleスキルを生成
---

skill-writerサブエージェントを起動して、以下のタスクを実行してください：

## タスク

$ARGUMENTS で提供されたパターンJSONから、article-templatesとwriting-styleスキルを生成してください。

## 入力データ

$ARGUMENTS

## スキル生成先パス（重要）

### プロジェクトルート検出

`.claude/`ディレクトリが存在するディレクトリをプロジェクトルートとする

### スキルファイルの生成先

プロジェクトルートからの相対パス:

1. **article-templates**:
   - .claude/skills/article-templates/SKILL.md
   - .claude/skills/article-templates/templates/qiita/{category}.md
   - .claude/skills/article-templates/templates/zenn-article/{category}.md
   - .claude/skills/article-templates/templates/zenn-book/{category}.md

2. **writing-style**:
   - .claude/skills/writing-style/SKILL.md
   - .claude/skills/writing-style/templates/format_rules.md
   - .claude/skills/writing-style/templates/wordings.md
   - .claude/skills/writing-style/templates/intro_outro.md
   - .claude/skills/writing-style/generated/format_rules.md
   - .claude/skills/writing-style/generated/wordings.md
   - .claude/skills/writing-style/generated/intro_outro.md

### 重要な注意点

- 記事分析用のディレクトリパス（qiita/articles/, zenn/articles/など）は分析対象であり、スキル生成先ではありません
- スキルは必ずプロジェクトルートの`.claude/skills/`配下に生成してください

**避けるべき間違ったパス**:
❌ qiita/articles/.claude/skills/
❌ zenn/articles/.claude/skills/

**正しいパス**:
✅ .claude/skills/（プロジェクトルート直下）

## 期待される出力

生成完了サマリー:
- 新規作成モード: 生成されたスキルのバージョンとファイル一覧
- 更新モード: 更新内容とバージョン変更の詳細
