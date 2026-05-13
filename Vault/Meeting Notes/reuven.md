# ראובן — מנכ"ל הצוות

## Overview
ראובן הוא המוח המרכזי של הצוות — הסוכן שמקבל בקשות מהמשתמש, מנתח אותן, ומחליט את מי מסוכני המשנה להפעיל. הוא **לא** sub-agent בקובץ נפרד; הוא מיוצג ישירות ע"י [[claude-md|CLAUDE.md]] בשורש הפרויקט (הקובץ עצמו הוא הזהות, הזיכרון וההוראות שלו). הצוות שמתחתיו: [[yael]], [[yuval]], [[chen]]. כל הסקילים תחת `.claude/skills/` זמינים לראובן ולסוכני המשנה (ראו [[superpowers-installation]]).

## Open Questions
- האם להוסיף סעיף "Common errors / Debugging" ב-CLAUDE.md אם יצוצו תקלות חוזרות?

## Session Log

### 2026-05-13 — Initial setup — Reuven defined via CLAUDE.md [shipped]
- **What was done:** נוצר `CLAUDE.md` בשורש הפרויקט עם הצגה עצמית של ראובן בגוף ראשון, תיאור הפרויקט, רשימת הצוות, ומבנה התיקיות `.claude/`.
- **Decisions:** ראובן לא יהיה sub-agent ב-`.claude/agents/` — הקובץ `CLAUDE.md` עצמו הוא הייצוג שלו. כך ההוראות שלו נטענות אוטומטית בכל סשן.
- **Notes / Caveats:** הוראות הניתוב המפורטות לסוכני המשנה עדיין לא נכתבו — זה הצעד הבא.
- **Related:** [[yael]], [[yuval]], [[chen]], [[project-infrastructure]]

### 2026-05-13 — CLAUDE.md hardened via /init [shipped]
- **What was done:** הוספו ל-CLAUDE.md ארבעה סעיפים חדשים: (א) "הפניות חשובות לתחילת סשן" — links ל-memory, vault entry, ולסקילים; (ב) "כללי-זהב והגבלות שאסור לשבור" — שישה gotchas שהצטברו לאורך הסשנים (Vault casing, מודל gpt-image-2 קבוע, .env בלי רווח אחרי =, dispatch fallback, ריבוי קבצי קלט, שפת ברירת מחדל); (ג) "תיאום עם סוכנים אחרים" — מחליף את "## הערה" הגנרי, מתאר checklist 4-נקודות לכל שינוי ארכיטקטוני; (ד) "Git workflow" — Remote, branch, conventions.
- **Decisions:** ה-Reuven persona נשמר (פתיחה בגוף ראשון). התוספות הן additive — לא מחליפות סעיפים קיימים אלא ממלאות פערים. סעיף "## הערה" הגנרי יצא — אין יותר placeholders ב-CLAUDE.md.
- **Notes / Caveats:** העברתי את הלקחים מהסשנים הקודמים (כולל מה ש-memory מציין ברמת behavior) ל-CLAUDE.md ברמת documentation — שלא יחמיצו אותם סשנים חדשים אם הם לא קוראים מ-memory לפני שמתחילים.
- **Related:** [[project-infrastructure]], [[yael]], [[yuval]], [[chen]]
