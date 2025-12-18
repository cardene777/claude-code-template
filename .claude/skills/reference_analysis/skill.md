---
name: reference_analysis
description: A framework for analyzing reference articles, documentation, and source code from a consistent perspective. Extracts structured information for use in subsequent outline design and writing phases. Used in Phase 1 (Content Analysis Phase) of the article-writer agent.
---

# Reference Analysis Framework (Skill)

This skill provides a framework for analyzing reference materials (articles, documentation, code) from a consistent perspective.
Used in Phase 1 (Content Analysis Phase) of the article-writer agent.

## 1. Purpose

Extract structured insights from source materials to inform new article creation:
- **Pattern A (Document-based)**: Official documentation, guides, specifications
- **Pattern B (Reference-based)**: Blog articles, tutorials, technical posts
- **Pattern C (Code-based)**: Source code, GitHub repositories, code snippets

This skill focuses on **analyzing external reference materials**, not your own articles.
For analyzing your own articles to extract patterns, use the `pattern_extraction` skill instead.

## 2. Analysis Prerequisites

Target materials are technical content for software engineers, assuming beginner to intermediate level readers.
The purpose of analysis is to organize information in a form that can be used for subsequent "outline design" and "new article writing".

## 3. Elements to Extract

### 3.1 Common Elements (All Patterns)

Extract the following elements from each reference material:

| Element | Content to Extract |
|---------|-------------------|
| **Theme and Claims** | Central theme, message the author wants to convey, target audience |
| **Problem** | Specific pain points addressed, context of occurrence, impact |
| **Solution Approach** | Proposed technologies/methods, key components, comparison with alternatives |
| **Code Examples** | Role of important code snippets, how to use APIs/libraries, implementation tips |
| **Prerequisites** | Expected prerequisite technologies, dependent tools/libraries/concepts |
| **Limitations** | Cases where the approach is not suitable, performance/maintainability/cost trade-offs |
| **Structural Techniques** | Section structure, storytelling techniques, use of diagrams and metaphors |

### 3.2 Additional Elements for Pattern C (Code-based)

When analyzing source code, also extract:

| Element | Content to Extract |
|---------|-------------------|
| **Architecture Overview** | High-level design, component relationships, data flow |
| **Key Functions** | Important functions/methods, their responsibilities, signatures |
| **State Variables** | Critical state management, data structures, persistence |
| **External Dependencies** | Libraries, frameworks, external services, APIs |
| **Security Considerations** | Access control, input validation, sensitive data handling |

## 4. Output Format

### 4.1 Pattern A & B Output (Documentation/Articles)

```json
{
  "source_id": "string",
  "source_type": "documentation | article | guide",
  "title": "string",
  "url": "string | null",
  "theme": "string",
  "main_claim": "string",
  "target_audience": "beginner | intermediate | advanced | mixed",
  "problems": [
    {
      "description": "string",
      "context": "string",
      "impact": "string"
    }
  ],
  "solutions": [
    {
      "summary": "string",
      "key_components": ["string"],
      "pros": ["string"],
      "cons": ["string"]
    }
  ],
  "code_highlights": [
    {
      "description": "string",
      "language": "string",
      "pseudo": "string"
    }
  ],
  "prerequisites": ["string"],
  "limitations": ["string"],
  "structural_techniques": {
    "sections": ["string"],
    "storytelling_techniques": ["string"]
  }
}
```

### 4.2 Pattern C Output (Code-based)

```json
{
  "source_id": "string",
  "source_type": "code",
  "repository_url": "string | null",
  "file_path": "string | null",
  "theme": "string",
  "main_claim": "string",
  "target_audience": "beginner | intermediate | advanced | mixed",
  "problems": [
    {
      "description": "string",
      "context": "string",
      "impact": "string"
    }
  ],
  "solutions": [
    {
      "summary": "string",
      "key_components": ["string"],
      "pros": ["string"],
      "cons": ["string"]
    }
  ],
  "code_highlights": [
    {
      "description": "string",
      "language": "string",
      "pseudo": "string"
    }
  ],
  "prerequisites": ["string"],
  "limitations": ["string"],
  "structural_techniques": {
    "sections": ["string"],
    "storytelling_techniques": ["string"]
  },
  "architecture_overview": {
    "design_pattern": "string",
    "component_relationships": ["string"],
    "data_flow": "string"
  },
  "key_functions": [
    {
      "name": "string",
      "responsibility": "string",
      "signature": "string",
      "important_notes": "string"
    }
  ],
  "state_variables": [
    {
      "name": "string",
      "purpose": "string",
      "type": "string"
    }
  ],
  "external_dependencies": [
    {
      "name": "string",
      "purpose": "string",
      "version": "string | null"
    }
  ],
  "security_considerations": ["string"]
}
```

## 5. Analysis Process

### 5.1 Pattern A & B (Documentation/Articles)

**Step 1: Gather Basic Information**
Check title, URL, publication date, article length, and platform.

**Step 2: Identify Theme and Claims**
Review the introduction and conclusion sections, and understand the overall picture from the heading structure.

**Step 3: Extract Problems**
Identify "why this content is needed" and articulate the problems readers face and their impact.

**Step 4: Analyze Solutions**
Identify proposed technologies/methods and organize key components and architecture.
Also collect comparison information with other alternatives.

**Step 5: Evaluate Code Examples**
Identify important code snippets and record the purpose/role and implementation points of each code.

**Step 6: Identify Prerequisites and Constraints**
List required prerequisite knowledge and clarify the limitations, constraints, and trade-offs of the approach.

**Step 7: Analyze Structure**
Record section structure, storytelling techniques, and use of diagrams and metaphors.

### 5.2 Pattern C (Code-based)

**Step 1: Gather Basic Information**
Check repository URL, file paths, programming language, and project structure.

**Step 2: Architecture Analysis**
Identify design patterns, component relationships, and data flow.
Use Kiri MCP for dependency analysis and semantic search.

**Step 3: Key Function Identification**
Extract important functions/methods, their responsibilities, and signatures.
Use `mcp__kiri__context_bundle` for efficient code context extraction.

**Step 4: State Management Analysis**
Identify state variables, data structures, and persistence mechanisms.

**Step 5: Dependency Analysis**
List external libraries, frameworks, and APIs.
Use `mcp__kiri__deps_closure` for dependency chain analysis.

**Step 6: Security Review**
Identify security considerations, access control, and sensitive data handling.

**Step 7: Extract Problems and Solutions**
Identify the problem the code solves and the solution approach taken.

**Step 8: Document Structural Insights**
Record how the code is organized, naming conventions, and architectural patterns.

## 6. Analysis Notes

**General Guidelines**:
- Do not copy-paste original expressions directly; summarize and abstract them
- Do not evaluate or criticize; faithfully extract facts and structure
- Do not guess unclear points; treat them as `null` or `"unknown"`
- When analyzing multiple sources, use parallel processing for efficiency

**Pattern C Specific**:
- Use Kiri MCP for semantic search and dependency analysis
- Focus on understanding the "why" behind code design decisions
- Extract reusable patterns and architectural insights
- Document security considerations and potential risks

## 7. Tool Usage

### 7.1 For Pattern A & B
- **WebFetch**: Fetch documentation and articles
- **WebSearch**: Supplement with background information
- **Context7 MCP**: Get structured library documentation

### 7.2 For Pattern C
- **GitHub MCP**: Access repositories, explore structure
- **Kiri MCP**: Semantic search, dependency analysis, context extraction
  - `mcp__kiri__context_bundle`: Auto-ranked code snippet extraction
  - `mcp__kiri__deps_closure`: Dependency chain analysis
  - `mcp__kiri__files_search`: Keyword-based file search
- **Read/Grep**: Basic file reading and search

## 8. Related Skills

- `pattern_extraction` - Analyzes your own articles to extract patterns (different purpose)
- `article_templates` - Used in the outline design phase (generated skill)
- `tone_guidelines` - Used in the writing phase (generated skill)

## 9. Differences from pattern_extraction

| Aspect | reference_analysis | pattern_extraction |
|--------|-------------------|-------------------|
| **Purpose** | Analyze external references for content understanding | Analyze your own articles for pattern extraction |
| **Input** | Documentation, blog articles, source code | Your own published articles |
| **Output** | Structured content insights (JSON) | Category patterns, tone patterns, templates (JSON) |
| **Used by** | article-writer agent (Phase 1) | template-generator agent |
| **Focus** | What the reference teaches | How you write articles |
