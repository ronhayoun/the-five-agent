# Skill: obsidian-vault-workflow

## Overview
סקיל מקומי תחת `.claude/skills/obsidian-vault-workflow/SKILL.md` שמגדיר את **הפרוטוקול המחייב** של ה-Vault: לפני כל משימה לקרוא את קובץ הטופיק הרלוונטי (Overview + Open Questions + כל Session Log), אחרי כל משימה לצרף רישום מתוארך עם status tag, ולעדכן Overview/Open Questions לפי הצורך. ההפעלה אוטומטית בכל סשן ובכל פקודה — מובטח ע"י הוראה ב-[[reuven|CLAUDE.md]]. הסקיל מגדיר את מבנה התיקיות (`Meeting Notes/`, `Content Briefs/`, `Publishing Log/`, `Brand Guidelines/`), פורמט topic-file, status tags, ו-anti-patterns.

## Open Questions
- האם נשתמש בכל ארבע תיקיות ה-vault (Meeting Notes, Content Briefs, Publishing Log, Brand Guidelines), או רק ב-Meeting Notes ל-MVP?
- האם להוסיף hook ב-`settings.json` שיאכוף את ההפעלה במקום להסתמך רק על CLAUDE.md?

## Session Log

### 2026-05-13 — Skill present, vault initialized [shipped]
- **What was done:** ה-SKILL.md הוצב ע"י המשתמש (קובץ קיים מראש — לא נוצר/נדרס). אותחלה תיקיית `Vault/Meeting Notes/` עם `_index.md` ו-8 קבצי topic ראשונים (סוכנים + קבצי תשתית). CLAUDE.md עודכן להזכיר את הסקיל כפרוטוקול חובה.
- **Decisions:** המשתמש בחר שלא לדרוס את SKILL.md הקיים — ההגדרה שלו (vault-as-memory) אומצה כפי שהיא.
- **Notes / Caveats:** המבנה `vault/` הוחלף ל-`Vault/` עם V גדולה כי כך git שמר את התיקייה. ב-Windows הקובץ גם וגם — case-insensitive.
- **Related:** [[reuven]], [[project-infrastructure]], [[skill-obsidian-markdown]], [[skill-obsidian-bases]]
