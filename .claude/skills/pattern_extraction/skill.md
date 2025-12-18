---
name: pattern_extraction
description: Extracts common patterns from a collection of your own articles to generate templates and style guidelines. Used by template-generator agent to analyze existing articles and create customized writing system.
---

# Pattern Extraction from Article Collection (Skill)

This skill analyzes multiple articles to identify common patterns, categorize them, and extract reusable structures.
Used by template-generator agent.

## 1. Purpose

Extract patterns from your own existing articles to generate:
- Category definitions
- Section structure templates
- Tone and style guidelines
- Writing conventions

## 2. Extraction Goals

### 2.1 Category Patterns

Group articles by content type based on what the article actually explains, not by:
- Author's introduction or self-description
- Company/organization mentioned
- Metadata or tags
- Title alone

**Categorization Process**:
1. Read entire article content (not just introduction or metadata)
2. Identify the main technical topic being explained
3. Determine article type based on structure:
   - Explainer: Explains a concept, technology, or standard
   - Hands-on/Tutorial: Step-by-step implementation guide
   - Case Study: Real-world implementation analysis
   - Reference: API documentation, specification summary
4. Group articles by primary topic (e.g., "ERC20 token standard", "React hooks")
5. Create category names that reflect the technical content pattern
6. Calculate category ratios (percentage of articles in each category)

### 2.2 Structure Patterns

Identify common section sequences:
- Introduction patterns
- Main content structure
- Code example placement
- Conclusion patterns

### 2.3 Tone Patterns

Extract writing style, expressions, formatting rules:
- Politeness level (desu/masu vs. da/dearu)
- Common expressions and phrases
- Technical terminology usage
- Sentence structure preferences

### 2.4 Code Patterns

Identify common code block usage:
- Code block frequency
- Language distribution
- Code explanation style
- Inline code vs. code blocks

## 3. Input Requirements

This skill expects a collection of your own articles:
- Minimum 10 articles recommended
- Articles from any platform (Qiita, Zenn, Medium, note, blog, etc.)
- Markdown format preferred

## 4. Output Format

Output analysis results in the following JSON format:

```json
{
  "analysis_metadata": {
    "total_articles": number,
    "platforms": {
      "platform_name": number
    },
    "analyzed_at": "YYYY-MM-DD HH:MM:SS"
  },
  "categories": [
    {
      "platform": "string",
      "category_name": "string",
      "article_count": number,
      "percentage": number,
      "section_patterns": ["string"],
      "average_sections": number,
      "common_section_names": ["string"]
    }
  ],
  "tone_patterns": {
    "writing_style": {
      "form": "desu/masu | da/dearu",
      "formality": "polite | casual | academic"
    },
    "common_expressions": ["string"],
    "formatting_rules": {
      "line_breaks": "string (e.g., 'after period', 'none')",
      "code_blocks": "string (e.g., 'with language tag', 'with filename')",
      "lists": "string (e.g., 'unordered', 'ordered')",
      "headings": "string (e.g., '## for main sections')"
    },
    "terminology": {
      "technical_terms": ["string"],
      "standardized_words": {
        "term": "preferred_usage"
      }
    }
  },
  "code_patterns": {
    "total_code_blocks": number,
    "average_per_article": number,
    "languages": {
      "language_name": {
        "count": number,
        "percentage": number
      }
    },
    "code_explanation_style": "string (e.g., 'inline comments', 'before block', 'after block')"
  },
  "platform_usage": {
    "platform_name": {
      "count": number,
      "percentage": number
    }
  },
  "intro_outro_patterns": {
    "introduction": {
      "common_starts": ["string"],
      "typical_length": "short | medium | long"
    },
    "conclusion": {
      "common_ends": ["string"],
      "typical_length": "short | medium | long"
    }
  }
}
```

## 5. Analysis Process

### Step 1: Article Collection
- Read all articles from specified directories
- Identify platform from directory structure or file metadata
- Count total articles per platform

### Step 2: Category Analysis
- Analyze each article's content
- Group by technical topic and article type
- Calculate category distribution

### Step 3: Structure Analysis
- Extract section headings from each article
- Identify common section sequences
- Calculate average section count per category

### Step 4: Tone Analysis
- Analyze sentence endings (desu/masu vs. da/dearu)
- Extract common expressions and phrases
- Identify formatting conventions

### Step 5: Code Analysis
- Count code blocks per article
- Identify programming languages used
- Analyze code explanation style

### Step 6: Pattern Consolidation
- Consolidate findings into JSON format
- Calculate statistics and percentages
- Identify outliers and special cases

## 6. Analysis Notes

**Content-Based Classification**:
- Focus on what the article explains, not author background
- Avoid categories like "XX company's articles"
- Prefer categories based on technical content (e.g., "Smart Contract Tutorials")

**Pattern Identification**:
- Look for patterns that appear in 20% or more of articles
- Document both common patterns and variations
- Note platform-specific differences

**Statistical Rigor**:
- Calculate percentages to identify dominant patterns
- Identify minimum thresholds for pattern significance
- Document edge cases

## 7. Related Skills

- `article-skill-generator` - Uses this skill's output to generate article_templates and tone_guidelines
- Generated `article_templates` - Created based on category patterns
- Generated `tone_guidelines` - Created based on tone patterns

## 8. Output Usage

The JSON output from this skill is used by:
1. `article-skill-generator` skill to generate:
   - article_templates skill
   - tone_guidelines skill
2. template-generator agent to:
   - Report analysis summary to user
   - Create category-specific templates
   - Generate writing guidelines
