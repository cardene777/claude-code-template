# 記事作成の例

## 例1: ドキュメントベース記事作成

**ユーザー依頼**:
「[技術標準名]のドキュメントを基に記事を書いてください。URL: [ドキュメントURL]」
<!-- Example: 「GraphQL仕様のドキュメントを基に記事を書いてください。URL: https://spec.graphql.org/」 -->

**実行フロー**:
1. **Phase 0**: WebFetchでドキュメント取得
2. **Phase 1**: `reference.md`の6要素フレームワークで分析
   - テーマ: [技術テーマ]
   - 課題: [解決する課題]
   - 解決策: [主要な概念/コンポーネント]
3. **Phase 2**: `article-templates`で[プラットフォーム] [記事形式]選択、アウトライン作成
4. **Phase 3**: `writing-style`に従って執筆
5. **Phase 4**: 品質チェック、ファイル書き込み

**出力**: `[platform]/[type]/[topic].md`
<!-- Example: `zenn/books/graphql-guide/01-introduction.md` -->

---

## 例2: 参考記事ベース記事作成

**ユーザー依頼**:
「[技術トピック]について、以下の記事を参考に執筆してください:
- [参考記事URL 1]
- [参考記事URL 2]」
<!-- Example: 「TypeScriptの型システムについて、以下の記事を参考に執筆してください:
- https://www.typescriptlang.org/docs/handbook/2/types-from-types.html
- https://type-level-typescript.com/」 -->

**実行フロー**:
1. **Phase 1**: WebFetchで複数の記事を取得、共通点と相違点を分析
2. **Phase 2**: `article-templates`で[プラットフォーム] [記事形式]選択
3. **Phase 3**: `writing-style`に従って執筆
4. **Phase 4**: 品質チェック

**出力**: `[platform]/[type]/[topic].md`
<!-- Example: `qiita/articles/typescript-advanced-types-tutorial.md` -->

---

## 例3: コードベース記事作成

**ユーザー依頼**:
「この[コードファイル]（[ファイルパス]）について解説記事を書いてください」
<!-- Example: 「このAPIクライアント（src/api/client.ts）について解説記事を書いてください」 -->

**実行フロー**:
1. **Phase 0**: Readツールでコード取得
2. **Phase 1**: コード構造分析（関数、クラス、型定義、主要ロジック）
3. **Phase 2**: `article-templates`で[プラットフォーム] [記事形式]選択
4. **Phase 3**: コード例を含めて執筆
5. **Phase 4**: 品質チェック

**出力**: `[platform]/[type]/[topic].md`
<!-- Example: `zenn/articles/api-client-implementation-analysis.md` -->

---

## 例4: 既存記事の更新（部分更新）

**ユーザー依頼**:
「[記事パス] の[セクション名]セクションを最新情報で更新してください」
<!-- Example: 「articles/docker-basics.md のマルチステージビルドセクションを最新情報で更新してください」 -->

**実行フロー**:
1. **Phase 0**: 既存記事読み込み、更新モード選択（部分更新）
2. **Phase 1**: [セクション]に関する最新情報を収集
3. **Phase 2**: [セクション]のみのアウトライン作成
4. **Phase 3**: 該当セクションを書き直し、既存コンテンツと統合
5. **Phase 4**: 品質チェック

**出力**: `[article_path]`（更新版）
<!-- Example: `articles/docker-basics.md`（更新版） -->

---

## 例5: 既存記事の更新（全面改訂）

**ユーザー依頼**:
「[記事パス] を全面的に改訂してください」
<!-- Example: 「articles/kubernetes-deployment.md を全面的に改訂してください」 -->

**実行フロー**:
1. **Phase 0**: 既存記事読み込み、更新モード選択（全面改訂）
2. **Phase 1**: 既存記事を参考資料として分析
3. **Phase 2**: 最新の`article-templates`で構造を再設計
4. **Phase 3**: 完全に新しいコンテンツを執筆
5. **Phase 4**: 品質チェック

**出力**: `[article_path]`（新バージョン）
<!-- Example: `articles/kubernetes-deployment.md`（新バージョン） -->
