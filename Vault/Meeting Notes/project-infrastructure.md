# Project Infrastructure

## Overview
המבנה הבסיסי של הפרויקט: `CLAUDE.md` בשורש (ייצוג של [[reuven]]), תיקיית `.claude/` עם שלוש תתי-תיקיות (`agents/`, `skills/`, `commands/`), קבצי תשתית ([[env-files]], [[gitignore]]), תיקיית `Vault/` (התיעוד הזה), ותיקיית `.obsidian/` (הגדרות אפליקציית Obsidian). ה-`.claude/agents/` וה-`.claude/commands/` עדיין ריקים (`.gitkeep`-only). ה-`.claude/skills/` מכיל שלושה סקילים פרויקטיאליים של Obsidian ([[skill-obsidian-vault-workflow]], [[skill-obsidian-markdown]], [[skill-obsidian-bases]]) + 14 סקילים מ-superpowers (ראו [[superpowers-installation]]).

## Open Questions
- האם נשמור את ה-`.gitkeep` ב-`agents/` ו-`commands/` או נסיר אותם כשנמלא את התיקיות בקבצים אמיתיים?
- האם `commands/` יקבל פקודות slash מותאמות בהמשך?

## Session Log

### 2026-05-13 — Bootstrap project structure [shipped]
- **What was done:** נוצרה תיקיית `.claude/` עם `agents/`, `skills/`, `commands/`. נוצר `CLAUDE.md` בשורש הפרויקט עם הצגה של ראובן. אותחל ריפו Git והקוד נדחף ל-`github.com/ronhayoun/the-five-agent`.
- **Decisions:** `.gitkeep` נוסף לתיקיות הריקות כדי שגיט יעקוב אחריהן. שמות התיקיות תואמים לקונבנציה של Claude Code (`.claude/agents`, `.claude/skills`, `.claude/commands`).
- **Notes / Caveats:** התיקיות עצמן נשמרות ריקות עד לסשנים הבאים שבהם נמלא אותן.
- **Related:** [[reuven]], [[env-files]], [[gitignore]], [[superpowers-installation]]
