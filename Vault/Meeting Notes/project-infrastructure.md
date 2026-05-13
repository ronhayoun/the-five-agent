# Project Infrastructure

## Overview
המבנה הבסיסי של הפרויקט: `CLAUDE.md` בשורש (ייצוג של [[reuven]]), תיקיית `.claude/` עם תתי-תיקיות (`agents/`, `skills/`, `commands/`), קבצי תשתית ([[env-files]], [[gitignore]]), תיקיית `Vault/` (התיעוד הזה), ותיקיית `.obsidian/` (הגדרות אפליקציית Obsidian).

`.claude/agents/` מכיל כעת **שני סוכנים פעילים**: [[yael]] ו-[[yuval]] (חן עוד לא). `.claude/commands/` עדיין ריקה. `.claude/skills/` מכיל ארבעה סקילים פרויקטיאליים ([[skill-obsidian-vault-workflow]], [[skill-obsidian-markdown]], [[skill-obsidian-bases]], [[skill-gpt-image-gen]]) + 14 סקילים מ-superpowers (ראו [[superpowers-installation]]).

בשורש הפרויקט גם תיקיות עבודה: `yael/` (סגנון + reference של יעל), `yuval/` (reference + outputs של יובל), `Content/` (קלט ליעל), `Output/` (תוצרים סופיים — MD + HTML + `images/<slug>/`).

## Open Questions
- האם נשמור את ה-`.gitkeep` ב-`commands/` או נסיר אותו כשנמלא אותה?
- האם `commands/` יקבל פקודות slash מותאמות בהמשך?
- חן — מתי תיכנס לפעולה? (זה הפיתוח הגדול הבא)

## Session Log

### 2026-05-13 — Bootstrap project structure [shipped]
- **What was done:** נוצרה תיקיית `.claude/` עם `agents/`, `skills/`, `commands/`. נוצר `CLAUDE.md` בשורש הפרויקט עם הצגה של ראובן. אותחל ריפו Git והקוד נדחף ל-`github.com/ronhayoun/the-five-agent`.
- **Decisions:** `.gitkeep` נוסף לתיקיות הריקות כדי שגיט יעקוב אחריהן. שמות התיקיות תואמים לקונבנציה של Claude Code (`.claude/agents`, `.claude/skills`, `.claude/commands`).
- **Notes / Caveats:** התיקיות עצמן נשמרות ריקות עד לסשנים הבאים שבהם נמלא אותן.
- **Related:** [[reuven]], [[env-files]], [[gitignore]], [[superpowers-installation]]

### 2026-05-13 — Yuval + image pipeline integrated [shipped]
- **What was done:** נוצרו תיקיות `yuval/`, `yuval/reference/`, `yuval/outputs/` (עם `.gitkeep`). נוסף [[skill-gpt-image-gen]] תחת `.claude/skills/`. הוסרו ה-comments מ-`OPENAI_API_KEY` ב-`.env` וב-`.env.example`. CLAUDE.md הורחב עם סעיף "Pipeline: מאמר עם תמונות" שמגדיר את ה-flow יעל→יובל→ראובן וההעתקה ל-`Output/images/<slug>/`. [[yael]] עודכנה לפזר `{{IMAGE_NEEDED: "..."}}` placeholders.
- **Decisions:** Output/ הופך self-contained — תמונות מועתקות מ-`yuval/outputs/` ל-`Output/images/<article-slug>/` בעת ההדבקה. אחראיות ההעתקה על ראובן (לא על יעל ולא על יובל) — שני הסוכנים נשארים מבודדים בתחום שלהם.
- **Notes / Caveats:** המעבר ל-pipeline אינטגרטיבי דורש מראובן לקרוא ל-Agent tool מספר פעמים (יעל פעם, יובל פעם פר תמונה) ולחבר את התוצאות. בלי delegation אמיתי, כל הארכיטקטורה קורסת — ראו `memory/feedback_dispatch_subagents.md`.
- **Related:** [[reuven]], [[yael]], [[yuval]], [[skill-gpt-image-gen]], [[env-files]]
