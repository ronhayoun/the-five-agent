# יובל — מעצב התמונות

## Overview
יובל הוא sub-agent ייעודי שיתמחה ביצירת ויזואלים, גרפיקה וקריאייטיב. הסוכן עדיין לא מוגדר — אין לו קובץ הגדרה תחת `.claude/agents/`. ראובן ([[reuven]]) מנתב אליו בקשות שדורשות ויזואל. צפוי להשתמש במפתחות API חיצוניים (OpenAI / Gemini / Nano Banana) שיוגדרו ב-[[env-files|.env]]. שותפים טבעיים: [[yael]] (תוכן + ויזואל יחד) ו-[[chen]] (חן מספקת רפרנסים, יובל מבצע).

## Open Questions
- איזה ספק לייצור תמונות יבחר ראשון — OpenAI (DALL-E / GPT-image), Gemini, או Nano Banana?
- האם יובל יחזיק כלי MCP ייעודי לעיצוב, או רק קריאות API ישירות?
- היכן יישמרו התמונות המופקות? (תיקיית `output/` בפרויקט? S3?)

## Session Log

### 2026-05-13 — Role placeholder created [planned]
- **What was done:** יובל מופיע ברשימת הצוות ב-CLAUDE.md ובאינדקס ה-vault. ב-`.env.example` שמורים placeholders ל-`OPENAI_API_KEY` ו-`GEMINI_API_KEY` כצפי לשימוש שלו.
- **Decisions:** טרם הוחלט על ספק תמונות, פרומפט מערכת, או רשימת כלים.
- **Notes / Caveats:** הסוכן ייכתב בהמשך הסדנה.
- **Related:** [[reuven]], [[yael]], [[chen]], [[env-files]]
