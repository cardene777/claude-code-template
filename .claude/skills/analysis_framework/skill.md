---
name: analysis_framework
description: A framework for analyzing technical articles from a consistent perspective. Extracts information from multiple reference articles and organizes it for use in subsequent outline design and writing phases. Used in Phase 1 (Article Analysis Phase) of the article-writer agent.
---

# Technical Article Analysis Framework (Skill)

This skill provides a framework for analyzing multiple technical articles from a consistent perspective.
Used in Phase 1 (Article Analysis Phase) of the article-writer agent.

## 1. Analysis Prerequisites

Target articles are technical articles for software engineers, assuming beginner to intermediate level readers.
The purpose of analysis is to organize information in a form that can be used for subsequent "outline design" and "new article writing".

## 2. Six Elements to Extract

Extract the following 6 elements from each article.

| Element | Content to Extract |
|---------|-------------------|
| **Theme and Claims** | Central theme of the article, message the author wants to convey, target audience |
| **Problem** | Specific pain points readers face, context of occurrence, impact |
| **Solution Approach** | Proposed technologies/methods, key components, comparison with alternatives |
| **Implementation/Code Examples** | Role of important code snippets, how to use APIs/libraries, implementation tips |
| **Prerequisites** | Expected prerequisite technologies, dependent tools/libraries/concepts |
| **Constraints/Trade-offs** | Cases where the approach is not suitable, performance/maintainability/cost trade-offs |

Also record structural and storytelling features (section structure, techniques to engage readers, use of diagrams and metaphors).

## 3. Output Format

Summarize analysis results in the following JSON format.

```json
{
  "article_id": "string",
  "title": "string",
  "url": "string | null",
  "theme": "string",
  "main_claim": "string",
  "target_audience": "beginner | intermediate | advanced | mixed",
  "problems": [
    { "description": "string", "context": "string", "impact": "string" }
  ],
  "solutions": [
    { "summary": "string", "key_components": ["string"], "pros": ["string"], "cons": ["string"] }
  ],
  "code_highlights": [
    { "description": "string", "language": "string", "pseudo": "string" }
  ],
  "prerequisites": ["string"],
  "limitations": ["string"],
  "structure_notes": {
    "sections": ["string"],
    "storytelling_techniques": ["string"]
  }
}
```

## 4. Analysis Process

**Step 1: Gather Basic Information**
Check title, URL, publication date, article length, and platform (Qiita, Zenn, etc.).

**Step 2: Identify Theme and Claims**
Review the introduction and conclusion sections, and understand the overall picture from the heading structure.

**Step 3: Extract Problems**
Identify "why this article is needed" and articulate the problems readers face and their impact.

**Step 4: Analyze Solutions**
Identify proposed technologies/methods and organize key components and architecture.
Also collect comparison information with other alternatives.

**Step 5: Evaluate Code Examples**
Identify important code snippets and record the purpose/role and implementation points of each code.

**Step 6: Identify Prerequisites and Constraints**
List required prerequisite knowledge and clarify the limitations, constraints, and trade-offs of the approach.

**Step 7: Analyze Structure**
Record section structure, storytelling techniques, and use of diagrams and metaphors.

## 5. Analysis Notes

Do not copy-paste original expressions directly; summarize and abstract them.
Do not evaluate or criticize; faithfully extract facts and structure.
Do not guess unclear points; treat them as `null` or `"unknown"`.
When analyzing multiple articles, use parallel processing for efficiency.

## 6. Related Skills

`article_templates` is used in the outline design phase, `tone_guidelines` is used in the writing phase.
