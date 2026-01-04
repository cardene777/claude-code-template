# テンプレート生成の例

## 例1: 初回生成（Create Mode）

**ユーザー依頼**:
「[platform_a]/articles/と[platform_b]/articles/のMarkdownファイルを分析してスキルを生成してください」
<!-- Example: 「qiita/articles/とzenn/articles/のMarkdownファイルを分析してスキルを生成してください」 -->

**実行フロー**:

1. **Phase 0: ディレクトリ確認**
   - ユーザー指定のディレクトリパスを解析
   - Globツールで `.md` ファイルを検索
   - プラットフォームを識別

2. **Phase 1: パターン抽出**
   - `scripts/pattern_extraction.md` のロジックを使用
   - すべての記事を読み込み
   - カテゴリ、構造、トーン、コードパターンを抽出
   - JSON形式で結果を整理

3. **ユーザーチェックポイント**
   - 分析結果を表示（カテゴリ分布、記事数、検出されたパターン）
   - ユーザーに承認を依頼

4. **Phase 2: スキル生成**
   - `scripts/skill_generator.md` のロジックを使用
   - article-templates skillを生成（SKILL.md + templates/）
   - writing-style skillを生成（SKILL.md + templates/ + generated/）
   - すべてのファイルを `.claude/skills/` に出力

5. **Phase 3: 検証とサマリー**
   - 生成されたファイルを確認
   - サマリーレポートを表示
   - 次のステップを案内

---

## 例2: 更新モード（Update Mode）

**ユーザー依頼**:
「新しい記事を追加したので、スキルを更新してください。[platform]/articles/を再分析してください」
<!-- Example: 「新しい記事を追加したので、スキルを更新してください。zenn/articles/を再分析してください」 -->

**実行フロー**:

1. **Phase 0: 既存スキル確認**
   - `.claude/skills/article-templates/SKILL.md` の存在を確認
   - `.claude/skills/writing-style/SKILL.md` の存在を確認
   - 更新モードを選択

2. **Phase 1: パターン抽出**
   - `scripts/pattern_extraction.md` のロジックを使用
   - 新しい記事を含めて再分析
   - 既存カテゴリと新規カテゴリを識別

3. **ユーザーチェックポイント**
   - 新しく検出されたカテゴリを表示
   - 既存カテゴリの記事数更新を表示
   - ユーザーに承認を依頼

4. **Phase 2: スキル更新**
   - `scripts/skill_generator.md` の更新ロジックを使用
   - 既存スキルを読み込み
   - 新しいパターンをマージ
   - `# CUSTOM` セクションを保持
   - バージョン番号をインクリメント

5. **Phase 3: 検証とサマリー**
   - 更新内容を表示（新規カテゴリ、更新されたカテゴリ）
   - 保持されたカスタムセクションを報告

---

## 例3: カスタムセクション保持

**シナリオ**:
ユーザーが `writing-style/templates/intro_outro.md` をカスタマイズ済み

**更新時の動作**:

1. **カスタマイズ前**（generated/intro_outro.mdの例）:
```markdown
## はじめに

[PERSONAL_LINKS]
<!-- Example:
https://example.com/author-profile
https://twitter.com/your_account
https://your-blog.com
-->

今回は「**[TOPIC]**」についてまとめていきます。
```

2. **ユーザーがtemplates/intro_outro.mdをカスタマイズ**:
```markdown
## はじめに

[GREETING]
<!-- Generated Example: [著者の挨拶] -->

[CUSTOM_LINKS]
<!-- 自分のSNSリンクをここに -->

[TOPIC_INTRODUCTION]
<!-- Generated Example: この記事では、[topic]について解説します。 -->

<!-- ========================================
     カスタムテンプレート追加エリア
     ======================================== -->

## カスタムイントロ

[CUSTOM_INTRO_TEXT]
<!-- Example: こんにちは、[著者名]です。
最近、[topic]について調べる機会がありました。 -->
```

3. **更新後**:
   - templates/ のカスタマイズは完全に保持される
   - generated/ のみ再生成される

---

## 例4: エラーハンドリング

**シナリオ1: ディレクトリが存在しない**

**ユーザー依頼**:
「invalid/path/を分析してください」

**実行結果**:
```
エラー: 指定されたディレクトリ 'invalid/path/' が見つかりません。

有効なディレクトリパスを指定してください。
例:
- [platform_a]/articles/
- [platform_b]/articles/
- [platform_c]/books/
```

---

**シナリオ2: 記事が少なすぎる**

**ユーザー依頼**:
「test/articles/を分析してください」（記事数: 3件）

**実行結果**:
```
警告: 分析された記事が少なすぎます（3記事）。

最低でも10記事以上を推奨します。
現在の記事数では、カテゴリ分類の精度が低くなる可能性があります。

続行しますか？
- はい: 分析を続行（汎用的なテンプレートを生成）
- いいえ: 記事を追加してから再実行
```

---

**シナリオ3: カテゴリが検出されない**

**実行結果**:
```
警告: 明確なカテゴリパターンが検出されませんでした。

汎用的な「Other」カテゴリを作成します。
より詳細なカテゴリ分類を行うには、以下を試してください:
1. 記事数を増やす（現在: 5記事 → 推奨: 10記事以上）
2. 記事のトピックを多様化する
3. 記事の構造を統一する
```

---

## 例5: 複数プラットフォーム分析

**ユーザー依頼**:
「[platform_a]/articles/, [platform_b]/articles/, [platform_c]/books/をすべて分析してください」
<!-- Example: 「qiita/articles/, zenn/articles/, zenn/books/をすべて分析してください」 -->

**実行フロー**:

1. **Phase 1: パターン抽出**
   - 各プラットフォームごとに記事を収集
   - プラットフォーム別にカテゴリを分析

   **結果例**:
   ```
   📊 分析結果

   プラットフォーム: [Platform A] ([N]記事)
   <!-- Example: Qiita (250記事) -->
   カテゴリ:
   - [Category 1]: [X]% ([M]記事)
     <!-- Example: API Documentation: 45.2% (113記事) -->
   - [Category 2]: [Y]% ([L]記事)
     <!-- Example: Tutorial Articles: 28.4% (71記事) -->
   - [Category 3]: [Z]% ([K]記事)
     <!-- Example: Technical Tips: 26.4% (66記事) -->

   プラットフォーム: [Platform B] ([N]記事)
   <!-- Example: Zenn Article (120記事) -->
   カテゴリ:
   - [Category 1]: [X]% ([M]記事)
     <!-- Example: Code Analysis: 40.0% (48記事) -->
   - [Category 2]: [Y]% ([L]記事)
     <!-- Example: Tool Introductions: 35.0% (42記事) -->
   - [Category 3]: [Z]% ([K]記事)
     <!-- Example: Concept Explainers: 25.0% (30記事) -->

   プラットフォーム: [Platform C] ([N]記事)
   <!-- Example: Zenn Book (15記事) -->
   カテゴリ:
   - [Category 1]: [X]% ([M]記事)
     <!-- Example: Comprehensive Guides: 66.7% (10記事) -->
   - [Category 2]: [Y]% ([L]記事)
     <!-- Example: Framework Deep Dives: 33.3% (5記事) -->
   ```

2. **Phase 2: スキル生成**
   - 各プラットフォーム用のテンプレートを生成
   - `templates/[platform_a]/`, `templates/[platform_b]/`, `templates/[platform_c]/`
   - プラットフォーム横断で共通のライティングスタイルガイドラインを生成

---

## トラブルシューティング

### 問題: 生成されたカテゴリが不正確

**原因**:
- 記事のメタデータのみで分類している
- 記事の本文を読んでいない

**解決策**:
- `scripts/pattern_extraction.md` のロジックを確認
- 全文を読み込んでコンテンツベースで分類することを確認

---

### 問題: カスタマイズが失われた

**原因**:
- `# CUSTOM` マーカーを使用していなかった

**解決策**:
- カスタマイズする前に `# CUSTOM` コメントを追加
- 次回更新時は保持される

---

### 問題: 日本語が文字化けする

**原因**:
- ファイルエンコーディングがUTF-8でない

**解決策**:
- すべてのMarkdownファイルをUTF-8で保存
- Writeツール使用時はUTF-8を指定
