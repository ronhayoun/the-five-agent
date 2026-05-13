# Env Files — `.env` ו-`.env.example`

## Overview
שני קבצים בשורש הפרויקט שמנהלים משתני סביבה: `.env` הוא המקומי עם הערכים האמיתיים (gitignored, ראו [[gitignore]]), ו-`.env.example` היא תבנית ציבורית עם placeholders ריקים (נדחפת ל-Git). שניהם משותפים לכל הצוות — `ANTHROPIC_API_KEY` כללי, וגם משתנים ייעודיים: `OPENAI_API_KEY`/`GEMINI_API_KEY` ל-[[yuval]], `PERPLEXITY_API_KEY`/`TAVILY_API_KEY` ל-[[chen]].

## Open Questions
- האם בפועל יידרש `ANTHROPIC_API_KEY` כשמריצים דרך Claude Code (שכבר מאומת)? אם לא — אולי כדאי להוריד אותו לחלוטין מהתבנית.
- אילו עוד שירותים חיצוניים נצטרך (אחסון תמונות, מסדי נתונים, וכו')?

## Session Log

### 2026-05-13 — Created env templates with gitignore protection [shipped]
- **What was done:** נוצרו `.env`, `.env.example`, ו-[[gitignore]]. `.env` מוסתר ע"י `.gitignore` (כלל `.env`). `.env.example` נדחף ל-Git כדי שמי שמשכפל את הריפו ידע אילו משתנים נדרשים.
- **Decisions:** התבנית מכילה placeholder ל-`ANTHROPIC_API_KEY` ועוד הערות (closed) עבור מפתחות שיובל וחן עשויים להזדקק להם.
- **Notes / Caveats:** `git status` אומת שה-`.env` באמת מוסתר.
- **Related:** [[gitignore]], [[yuval]], [[chen]], [[reuven]]
