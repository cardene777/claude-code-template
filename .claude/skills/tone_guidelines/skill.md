---
name: tone_guidelines
description: Tone and style guidelines for writing technical articles. Used in Phase 3 (Writing Phase) of the article-writer agent. Provides rules for maintaining consistency in writing style, expressions, and formatting.
---

# Tone and Style Guidelines (Skill)

This skill provides guidelines for tone and style when writing technical articles.
Used in Phase 3 (Writing Phase) of the article-writer agent.

---

## 1. Public Article Principles (Most Important)

All articles and Books are published externally.
Never include local file paths (`.claude/skills/...`, `/Users/...`), internal work notes, or project-specific internal information.
When references are needed, use official documentation or GitHub URLs that readers can access.
Always ask yourself "Is this information valuable to readers?"

---

## 2. Title Rules

Keep article titles short and simple, aiming for under 30 characters.
Avoid subtitle formats that split titles with ":" or "：".

| Rating | Example |
|--------|---------|
| Good | "Circle's StableFX for On-chain FX", "Understanding ERC20 Basics" |
| Bad | "Circle StableFX: How the On-chain FX Engine Works and Its Possibilities" |

---

## 3. Writing Style Rules

Use **desu/masu form** (polite Japanese) consistently.

| Type | Recommended | Prohibited |
|------|-------------|------------|
| Explanations | "〜です", "〜ます", "〜していきます" | "〜である", "〜だ" (academic style) |
| Addressing readers | "〜ですよね", "〜してみてください" | "〜だよ", "〜じゃん" (overly casual) |
| Technical facts | Clear assertions | "多分〜", "〜かもしれません" (vague) |

---

## 4. Platform-Specific Differences

| Item | Qiita | Zenn |
|------|-------|------|
| Metadata | `tags: Tag1 Tag2 Tag3` | `topics: ["tag1", "tag2"]` |
| Message blocks | `:::note info/warn/alert` | `:::message` / `:::message alert` |
| Collapsible | Not supported | `:::details Title` |
| Solidity code | `js` (due to limitations) | `solidity` |
| Link placement | Place outside `:::note` blocks | No restrictions |

---

## 5. Format Rules

### 5.1 Period and Line Break Rules

Always break line after a sentence ends with Japanese period (。).
Do not continue multiple sentences on the same line.
However, only add a line break after period, not a blank line.

### 5.2 No Colon at End

Do not end sentences with colon (:).
When continuing explanation after a label, break line and describe.

```markdown
❌ **Read Tool**: Reads file contents
✅ **Read Tool**
   Reads file contents.
```

Exception: Colons can be used in field definitions (`title: Article Title`).

### 5.3 Bold Inside Japanese Brackets

Text inside 「」 must always be bold.
Example: 今回は「**統一されたトークンの規格**」についてまとめていきます。

### 5.4 Code Blocks

Always specify language and filename for code blocks.
For Solidity code, use `js` on Qiita and `solidity` on Zenn.

````markdown
```typescript:src/components/Button.tsx
export const Button = () => <button>Click</button>;
```
````

### 5.5 Use "時" Instead of "際"

"ファイルを読み込む際は" → "ファイルを読み込む時は"

---

## 6. Blank Line Rules

Add blank lines before and after headings, code blocks, lists, URLs, and message blocks.
Do not add blank lines between list items or between regular paragraph text.

---

## 7. Heading Rules

Do not include explanatory text in headings; explain in the first sentence of the body.
Bold marks (`**`) are not needed inside heading tags (they are automatically bold).
Only number headings for work procedures like Step 1, Step 2.

```markdown
❌ ### Tools - Functions that LLMs can execute
✅ ### Tools
   Tools are functions that LLMs can call to perform specific actions.
```

Sub-items like "Conditions" or "Notes" in function descriptions should use **bold** instead of heading tags.

---

## 8. Emphasis Rules

Use bold only for truly important keywords, first occurrence of technical terms (once only), and notes that must not be overlooked.
Do not use for labels ("Parameters", "Usage Examples", etc.) or words in regular explanatory text.

When parentheses follow bold text, add a half-width space after the closing parenthesis.
Example: **completed** status

---

## 9. Inline Code Rules

Wrap function names (`transfer()`), variable names (`_to`), file names (`SKILL.md`), and type names (`address` type) in backticks.
Add a half-width space between backtick-wrapped code elements and Japanese text.

```markdown
✅ `_to` で指定されたアドレスに送付する
❌ `_to`で指定されたアドレスに送付する
```

Exception: Do not add space immediately before punctuation (、。).

---

## 10. List Rules

Use numbered lists only when procedures or steps are clearly defined.
Use bullet lists (unordered) for enumerating features or describing characteristics.

Do not use colon (:) after bold labels; break line and then describe.

```markdown
✅ 1. **Create Task**
      Organize work content using the TodoWrite tool.
❌ 1. **Create Task**: Organize work content using the TodoWrite tool.
```

---

## 11. Item Separation Rules

When explaining multiple items, structure with **bold item name + description** instead of continuous sentences like "First〜", "Next〜", "Finally〜".
Separate items with blank lines, but do not use double blank lines.

```markdown
✅ **Recommendation and Reason**
   Present recommendation level (5-star rating) and reason for choices.

   **Clear and Specific Questions**
   Asking specific questions instead of vague ones makes them easier to answer.

❌ First, it's important to present recommendation level and reason for choices.
   Next, it's important to make questions clear and specific.
```

---

## 12. URL Placement Rules

Do not embed URLs in text; always place them on independent lines.
On Zenn and Qiita, URLs on independent lines display as link cards.

```markdown
✅ Access Anthropic Console.

   https://console.anthropic.com/

❌ Access Anthropic Console (https://console.anthropic.com/)
```

Exception: Markdown format links `[Text](URL)` can be placed in text.

---

## 13. Message Block Syntax

**Qiita**: Use `:::note info`, `:::note warn`, `:::note alert`.
Place Qiita links outside `:::note` blocks.

**Zenn**: Use `:::message`, `:::message alert`, `:::message warn`, `:::details Title`.

---

## 14. Terminology Standardization

| Recommended | Avoid |
|-------------|-------|
| スマートコントラクト | スマコン |
| ブロックチェーン | BC |
| 送付 | 転送 (as translation of transfer) |
| **ERC20**, **ERC721** | ERC20, ERC721 (bold required) |
| ユーザー | ユーザ |
| 〜の時 | 〜の際 |

Wrap code elements (Event, Struct, Modifier) in backticks (e.g., `Transfer` event).

---

## 15. Images and Screenshots

Use PNG (screenshots), JPG (photos), SVG (diagrams).
Maximum width 1200px, file size under 1MB recommended.
Alt text is required; add descriptive captions.

---

## 16. Numbers and Units

Use half-width numbers; use comma for thousands separator (`1,000`).
No space between number and % for percentages (`50%`); space between number and unit for size/capacity (`8 GB`).

---

## 17. Accessibility

Add alt text to all images.
Use text that describes the destination for links instead of "here" or "click here".
Keep heading structure logically hierarchical, following H1→H2→H3 order.

---

## 18. Quality Checklist

After writing, verify the following:

| Category | Check Items |
|----------|-------------|
| Writing style | Consistent desu/masu form, no casual/academic expressions |
| Format | Line break after period, no colon at end of line, bold inside brackets, language and filename in code blocks |
| Prohibited | No local file paths |
| Headings | No explanatory text, appropriate levels, no bold marks |
| Code elements | Use backticks, space between Japanese text |
| Platform | Correct Solidity language tag, correct message block syntax, URLs on independent lines |

---

## 19. Intro/Outro Templates

Fixed introduction and conclusion templates are defined in a separate file.
See `intro_outro.md` in this directory for the templates.

> **Note**: This is a CUSTOM file. Replace placeholders with your own information.

---

## 20. Related Skills

`analysis_framework` is used in the article analysis phase, `article_templates` is used in the outline design phase.
