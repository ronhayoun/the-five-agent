# חן — החוקרת

## Overview
חן היא sub-agent ייעודי שתתמחה באיסוף מידע, מחקר ואימות עובדות. הסוכן עדיין לא מוגדר — אין לה קובץ הגדרה תחת `.claude/agents/`. ראובן ([[reuven]]) מנתב אליה בקשות שדורשות מחקר/אימות. צפויה להשתמש במפתחות API חיצוניים (Perplexity / Tavily) שיוגדרו ב-[[env-files|.env]]. השותפויות שלה: היא ה-upstream של [[yael]] (מספקת חומר גלם לכתיבה) ושל [[yuval]] (מספקת רפרנסים ויזואליים).

## Open Questions
- איזה כלי חיפוש יהיה ברירת המחדל — Perplexity, Tavily, או WebFetch של Claude Code?
- האם תהיה לה גישה לקריאת PDF / מסמכים מקומיים, או רק לחיפוש ברשת?
- איך תפלוט תוצאות? (סיכום קצר, מאגר ציטוטים, או דוח מובנה)

## Session Log

### 2026-05-13 — Role placeholder created [planned]
- **What was done:** חן מופיעה ברשימת הצוות ב-CLAUDE.md ובאינדקס ה-vault. ב-`.env.example` שמורים placeholders ל-`PERPLEXITY_API_KEY` ו-`TAVILY_API_KEY` כצפי לשימוש שלה.
- **Decisions:** טרם הוחלט על ספק חיפוש, פרומפט מערכת, או רשימת כלים.
- **Notes / Caveats:** הסוכן ייכתב בהמשך הסדנה.
- **Related:** [[reuven]], [[yael]], [[yuval]], [[env-files]]
