---
name: mistake-recorder
description: Use when task completed with corrected errors - prompt user to record mistakes or starting new development - check .mistake-notebook.md for related past mistakes.
---

# Mistake Recorder

## Quick Start

**Recording a mistake:**
1. Append entry to .mistake-notebook.md (create if not exists)
2. Format: Date - Brief Description, with Error Phenomenon, Root Cause, How to Correct

**Checking past mistakes:**
1. Read .mistake-notebook.md if exists
2. Look for related past mistakes before new development

## Pre-Development Check (MANDATORY)

Before any new feature development or bug fix:
1. Check if .mistake-notebook.md exists
2. Read it to identify related past mistakes
3. Apply lessons to avoid repeating

## Recording Modes

### Quick Record

For single, clear mistakes. Invocation: user says "quick record", "log mistake", or AI detects correction during task completion.

```markdown
## [Date] - [Brief Error]

### Error Phenomenon
[One-line description]

### Error Root Cause
[One-sentence cause]

### How to Correct
[One-sentence solution]
```

### Standard Record

For complex or multiple mistakes. Invocation: user explicitly requests "record this mistake".

1. Summarize errors from context
2. Ask user confirmation: "Record? [Yes/Skip/Edit]"
3. Append to .mistake-notebook.md

## File Format

```markdown
# Mistake Notebook

Recording AI Agent development mistakes and correction experiences.

---

## [Date] - [Brief Description]

### Error Phenomenon

[Describe the specific manifestation]

### Error Root Cause

[Analyze the fundamental cause]

### How to Correct

[Describe the correct solution]

---
```

## Examples

**Quick Record:**
```
User: quick record this parameter mistake
AI: Records single error to .mistake-notebook.md ✓
```

**Standard Record:**
```
User: record this
AI: Summarizes error, confirms with user, records to file
```
