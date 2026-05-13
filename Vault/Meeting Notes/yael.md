# יעל — כותבת התוכן

## Overview
יעל היא sub-agent **פעיל** בצוות — כותבת התוכן. קובץ ההגדרה ב-`.claude/agents/yael.md`. תפקידה: לקחת מאמרי גלם מתיקיית `Content/` ולשכתב אותם בסגנון הפרויקט, ולהוציא שני תוצרים ל-`Output/` (גרסת Markdown + גרסת HTML עצמאית ב-RTL). הכלים שלה: `Read, Write, Edit, Glob, Grep` בלבד — אין לה Bash, Web, או יכולת להפעיל סוכנים אחרים. סגנון הכתיבה שלה מוגדר ב-`yael/style-guide.md` (טרם נכתב — תיכתב בהמשך ע"י המשתמש) ובדוגמאות ב-`yael/reference/`. ראובן ([[reuven]]) מנתב אליה דרך מילות מפתח שמוגדרות ב-CLAUDE.md (שכתב/ערוך/תרגם/סכם וכו'). שותפים טבעיים בעתיד: [[yuval]] (תוכן + ויזואל) ו-[[chen]] (חן מספקת מחקר, יעל מנסחת).

## Open Questions
- האם להוסיף תמיכה בקלט מ-`.txt`/`.docx`, או רק `.md`? (כרגע ה-prompt מציין `.md` + `.txt` בסיסי)
- מה ההתנהגות הרצויה אם `Content/` מכיל יותר ממאמר אחד ללא הוראה ספציפית? (כרגע: לבקש הבהרה מראובן)
- האם להפיק גם גרסת `.pdf` בעתיד? (יידרש כלי חיצוני — לא במסגרת הכלים הנוכחיים שלה)

## Session Log

### 2026-05-13 — Role placeholder created [planned]
- **What was done:** יעל מופיעה ברשימת הצוות ב-CLAUDE.md ובאינדקס ה-vault. לא נוצר עדיין קובץ הגדרה אמיתי תחת `.claude/agents/yael.md`.
- **Decisions:** טרם הוחלט על מודל בסיס, פרומפט מערכת, או רשימת כלים.
- **Notes / Caveats:** הסוכן ייכתב בהמשך הסדנה.
- **Related:** [[reuven]], [[yuval]], [[chen]], [[project-infrastructure]]

### 2026-05-13 — Yael agent activated [shipped]
- **What was done:** נכתב קובץ ההגדרה `.claude/agents/yael.md` עם YAML frontmatter (`name: yael`, `tools: Read, Write, Edit, Glob, Grep`, description עם trigger keywords בעברית ובאנגלית) ו-system prompt מלא בעברית (זהות, Flow, כללי שכתוב, תבנית HTML, מה היא יודעת ולא יודעת). נוצרו תיקיות עבודה בשורש: `yael/` (+ `yael/reference/`), `Content/`, `Output/` — כולן עם `.gitkeep`. CLAUDE.md עודכן: סעיף "## הערה" הקודם הוחלף ב-"## ניתוב לסוכני משנה" שמתאר את התנאים להפעלת יעל ומסמן את יובל וחן כ-placeholders.
- **Decisions:**
  - לא לציין `model` ב-frontmatter — יעל יורשת מאב (ראובן), משאיר גמישות.
  - HTML output: מסמך קלאסי קריא ב-RTL, inline CSS, רוחב ~720px, פונטים סריפיים-עבריים, line-height 1.7 (לפי בחירת המשתמש מתוך 3 אפשרויות).
  - לא לדרוס `yael/style-guide.md` — המשתמש יצור אותו בנפרד. ה-prompt מטפל גרציפלי במצב שהקובץ חסר ("style-guide טרם נכתב — כתבתי לפי שיקול דעת סביר").
  - כללי הסרת קישורים/CTAs מוגדרים מפורשות ב-prompt עם עיקרון מנחה ("סיפור נשאר, פלטפורמת מחבר מוסרת").
- **Notes / Caveats:** יעל יורשת את כל ה-17 סקילים תחת `.claude/skills/` — שימושי במיוחד `writing-skills` ו-`obsidian-markdown`. ה-HTML מומר ידנית מ-Markdown (אין לה כלי המרה).
- **Related:** [[reuven]], [[project-infrastructure]], [[skill-obsidian-markdown]], [[yuval]], [[chen]]
