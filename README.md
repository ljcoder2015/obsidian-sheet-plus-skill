# Obsidian Sheet Plus Skill

A pure Skill reference package for AI tools (TRAE, Claude Code, Cursor, Codex, OpenCode, Copilot CLI, Gemini CLI) to operate Obsidian Sheet Plus spreadsheets directly via REST API after loading.

## Installation

Clone into the project-level skills directory of your AI tool:

```bash
git clone git@github.com:ljcoder2015/obsidian-sheet-plus-skill.git
```

**TRAE:**
```bash
git clone git@github.com:ljcoder2015/obsidian-sheet-plus-skill.git .trae-cn/skills/obsidian-sheet-plus
```

**Claude Code:**
```bash
git clone git@github.com:ljcoder2015/obsidian-sheet-plus-skill.git .claude/skills/obsidian-sheet-plus
```

**Cursor:**
```bash
git clone git@github.com:ljcoder2015/obsidian-sheet-plus-skill.git .cursor/skills/obsidian-sheet-plus
```

**Codex (OpenAI):**
```bash
git clone git@github.com:ljcoder2015/obsidian-sheet-plus-skill.git .codex/skills/obsidian-sheet-plus
```

**OpenCode:**
```bash
git clone git@github.com:ljcoder2015/obsidian-sheet-plus-skill.git .opencode/skills/obsidian-sheet-plus
```

**Copilot CLI (GitHub):**
```bash
git clone git@github.com:ljcoder2015/obsidian-sheet-plus-skill.git .github/skills/obsidian-sheet-plus
```

**Gemini CLI (Google):**
```bash
git clone git@github.com:ljcoder2015/obsidian-sheet-plus-skill.git .gemini/skills/obsidian-sheet-plus
```

## Prerequisites

1. Obsidian is running
2. The **Sheet Plus** plugin is installed and enabled
3. The REST API service within the plugin is started (default port 3000)

## Usage

After the AI loads this skill, it will automatically recognize spreadsheet operation needs and execute them via the REST API. No additional configuration is required.

## Covered APIs

A total of 30 REST API endpoints, covering reading, writing, formulas, styles, data validation, filtering, conditional formatting, row/column operations, and cell merging.
