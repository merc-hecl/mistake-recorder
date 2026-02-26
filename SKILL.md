---
name: mistake-recorder
description: Records AI Agent mistakes and corrections to mistake-notebook.md after user acceptance. Prompts AI to check past mistakes before development. Triggers when: (1) User corrects AI's implementation and accepts; (2) Task completed after error correction.
---

# Mistake Recorder

## Overview

This skill helps record mistakes made by AI Agent during development and their correction methods after task completion, forming a "mistake notebook" for future reference and avoiding repeated errors.

## Pre-Development Check

**Before starting any feature development or coding task:**

1. Check if `mistake-notebook.md` exists in the working directory
2. If it exists, read through it to identify any past mistakes related to the current task
3. Pay special attention to:
   - Similar feature implementations
   - Related technologies or frameworks
   - Common patterns that caused issues before
4. Apply lessons learned to avoid repeating the same mistakes

This proactive check helps prevent recurring errors and improves code quality.

## Trigger Conditions (Post-Development)

This skill triggers when:

1. **Complete correction workflow ends**: User requests feature → AI Agent completes development → User points out implementation or logic error → AI Agent corrects → User accepts
2. **User explicitly confirms task completion**: User says "done", "looks good", "accepted", etc.

## Workflow

### Step 1: Confirm Recording

After task acceptance, ask the user:

```
Some errors occurred and were corrected during this development. Would you like to record these mistakes to mistake-notebook.md?
```

If user agrees, proceed to next step; if user declines, end this skill.

### Step 2: Summarize Error Information

Based on the conversation history, summarize the following:

1. **Error Phenomenon**: What was the specific manifestation of the error? How was it discovered?
2. **Error Root Cause**: What was the fundamental cause? Was it misunderstanding, logic error, or technical implementation issue?
3. **How to Correct**: How was the problem resolved? What was the correct implementation approach?

Present the summary to the user for confirmation. If the user has corrections or additions, update accordingly.

### Step 3: Write Record

**Important: Always APPEND to the file, never overwrite existing content.**

1. If `mistake-notebook.md` does not exist, create it with the following header:

```markdown
# Mistake Notebook

Recording AI Agent development mistakes and correction experiences.

---

```

2. Append the collected information to `mistake-notebook.md` using this format:

```markdown
## [Date] - [Brief Description]

### Error Phenomenon

[Describe the specific manifestation of the error]

### Error Root Cause

[Analyze the fundamental cause of the error]

### How to Correct

[Describe the correct solution and implementation approach]

---
```

### Step 4: Confirm Completion

Notify user that recording is complete and display a summary of the recorded content.

## Notes

- Keep records concise and clear, avoid redundant descriptions
- If multiple independent errors occurred during one development session, record them separately
- Respect user's wishes; do not force recording if user doesn't want certain errors recorded

## File Format Example

Example structure of `mistake-notebook.md`:

```markdown
# Mistake Notebook

Recording AI Agent development mistakes and correction experiences.

---

## 2024-01-15 - State Management Logic Error

### Error Phenomenon

User feedback: After clicking the delete button, the list data did not update correctly. Manual page refresh was required to see changes.

### Error Root Cause

After the delete operation completed, only the API was called to delete data, but local state was not synchronized. Incorrectly assumed the page would automatically refresh after successful API call.

### How to Correct

After successful delete API call, immediately remove the corresponding data item from local state to ensure UI and data synchronization. The correct approach is to execute state update in the then callback.

---

## 2024-01-20 - API Parameter Passing Error

### Error Phenomenon

Pagination not working properly. Regardless of which page was clicked, only the first page's data was displayed.

### Error Root Cause

When passing pagination parameter as query parameter, incorrectly used POST request body format, causing backend to fail parsing the pagination parameter.

### How to Correct

Correctly append pagination parameters to URL query string to ensure backend can parse them properly. Also check API documentation to confirm parameter passing method.

---
```
