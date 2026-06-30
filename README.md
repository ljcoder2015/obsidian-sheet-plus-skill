# Obsidian Sheet Plus Skill

A pure Skill reference package for AI tools (TRAE, Claude Code, Cursor, Codex, OpenCode, Copilot CLI, Gemini CLI) to operate Obsidian Sheet Plus spreadsheets directly via REST API after loading.

## Installation

Copy this directory into the AI tool's skills directory:

**TRAE:**
```bash
cp -r apps/obsidian-sheet-plus-skill ~/.trae-cn/skills/obsidian-sheet-plus
```

**Claude Code:**
```bash
cp -r apps/obsidian-sheet-plus-skill ~/.claude/skills/obsidian-sheet-plus
```

**Cursor:**
```bash
cp -r apps/obsidian-sheet-plus-skill ~/.cursor/skills/obsidian-sheet-plus
```

**Codex (OpenAI):**
```bash
cp -r apps/obsidian-sheet-plus-skill ~/.codex/skills/obsidian-sheet-plus
```

**OpenCode:**
```bash
cp -r apps/obsidian-sheet-plus-skill ~/.config/opencode/skills/obsidian-sheet-plus
```

**Copilot CLI (GitHub):**
```bash
cp -r apps/obsidian-sheet-plus-skill ~/.copilot/skills/obsidian-sheet-plus
```

**Gemini CLI (Google):**
```bash
cp -r apps/obsidian-sheet-plus-skill ~/.gemini/skills/obsidian-sheet-plus
```

> **Note:** SKILL.md format is compatible across all these tools. Install once, use everywhere. Some tools also support project-level installation (e.g., `.claude/skills/`, `.github/skills/`, `.gemini/skills/` inside your repo).

## Prerequisites

1. Obsidian is running
2. The **Sheet Plus** plugin is installed and enabled
3. The REST API service within the plugin is started (default port 3000)

## Usage

After the AI loads this skill, it will automatically recognize spreadsheet operation needs and execute them via the REST API. No additional configuration is required.

## Covered APIs

A total of 30 REST API endpoints, covering reading, writing, formulas, styles, data validation, filtering, conditional formatting, row/column operations, and cell merging.
