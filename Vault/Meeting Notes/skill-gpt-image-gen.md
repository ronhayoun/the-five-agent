# Skill: gpt-image-gen

## Overview
סקיל מקומי תחת `.claude/skills/gpt-image-gen/SKILL.md` שמספק מעטפת לקריאת OpenAI Images API. הסקיל מגדיר: שם המודל (`gpt-image-2` — קבוע, אסור לשנות), פרמטרי ברירת מחדל (1024x1024, medium, png), טמפלייט bash מלא (curl + jq decode + python fallback + source `.env` אוטומטי), Python-only fallback מלא, וטבלת שגיאות נפוצות. הסקיל הוא ה-API contract של [[yuval]] מול OpenAI — יובל קורא אותו בכל הפעלה.

## Open Questions
- האם להוסיף תמיכה ב-`size: 1024x1536` (portrait) או `1536x1024` (landscape) כברירת מחדל לסוגי תוכן שונים? (כרגע default = square)
- האם לפצל את הסקיל לפעולות נפרדות (`generate`, `edit`, `variations`) כשנוסיף תמיכה בעריכת תמונות קיימות?

## Session Log

### 2026-05-13 — Skill created for OpenAI gpt-image-2 [shipped]
- **What was done:** נכתב SKILL.md תחת `.claude/skills/gpt-image-gen/`. ה-frontmatter כולל triggers (generate/create/illustrate/draw + image/picture/visual). הגוף: אזהרה בולטת על שם המודל, טבלת default parameters, full bash template (source .env → curl → jq/python decode → verify), Python-only alternative, וטבלת שגיאות (401/400/429/empty file/wrong model).
- **Decisions:**
  - **שם המודל:** `gpt-image-2`. אזהרה בולטת כי הוא יצא 21-04-2026 וייתכן שלא מוכר ב-training cutoff. **אסור** להציע אלטרנטיבות.
  - **Decode:** עדיפות ל-jq, נפילה ל-python כי jq לא תמיד מותקן ב-Git Bash על Windows.
  - **`.env` sourcing:** אוטומטי בתחילת הסקריפט (`set -a && . ./.env && set +a`) אם `$OPENAI_API_KEY` ריק.
  - **Error handling:** check ל-`"error"` ב-response לפני decode, אימות size > 0 בקובץ הסופי.
- **Notes / Caveats:** כל המשתמשים של הסקיל ([[yuval]]) צריכים לקרוא אותו בתחילת כל הפעלה — לא להניח שהוא בזיכרון. רק שמעטפת ה-API מוגדרת כאן; ה-prompt-engineering עצמו אצל יובל.
- **Related:** [[yuval]], [[env-files]], [[project-infrastructure]]
