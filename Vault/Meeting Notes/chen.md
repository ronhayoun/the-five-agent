# חן — חוקרת הרשת

## Overview
חן היא sub-agent **פעיל** של חוקרת הרשת. קובץ ההגדרה ב-`.claude/agents/chen.md`. תפקידה: לקבל בקשה מראובן, לבדוק את הזיכרון הפרסיסטנטי שלה (`chen/Memory/searches.md`) כדי למנוע חיפושים כפולים, ולחפש ברשת מקור איכותי באמצעות `WebSearch` + `WebFetch`. היא מסננת לפי קריטריונים נוקשים (מקורות ראשוניים, פרסומים מקצועיים, פרסום בשנה האחרונה, ללא clickbait/אגרגטורים) ושומרת extract נקי ב-`Content/<YYYY-MM-DD>-<slug>.md` עם frontmatter מטא-נתונים (URL, איכות, dynamic boolean). הכלים שלה: `WebSearch, WebFetch, Read, Write, Edit, Glob, Grep` — **אין** Bash ו**אין** API חיצוני. שותפויות: היא ה-upstream של [[yael]] (מכינה את הקלט שלה); אין לה אינטראקציה ישירה עם [[yuval]]. **ארכיטקטונית קריטית:** חן לא קוראת ליעל. ראובן מחליט אם להמשיך ב-pipeline.

## Open Questions
- עד כמה אגרסיבי dedupe להיות? כרגע 30 ימים על נושאים יציבים — להוריד / להעלות?
- איך לטפל ב-paywalled sources באופן עקבי? (כרגע: דלגי וחפשי אלטרנטיבה)
- האם להוסיף סינון לפי שפה (העדפה לעברית כשהקהל ישראלי)? כרגע אד-הוק לפי שיקול דעת.

## Session Log

### 2026-05-13 — Role placeholder created [planned]
- **What was done:** חן מופיעה ברשימת הצוות ב-CLAUDE.md ובאינדקס ה-vault. ב-`.env.example` שמורים placeholders ל-`PERPLEXITY_API_KEY` ו-`TAVILY_API_KEY` כצפי לשימוש שלה.
- **Decisions:** טרם הוחלט על ספק חיפוש, פרומפט מערכת, או רשימת כלים.
- **Notes / Caveats:** הסוכן ייכתב בהמשך הסדנה.
- **Related:** [[reuven]], [[yael]], [[yuval]], [[env-files]]

### 2026-05-13 — Chen agent activated [shipped]
- **What was done:** נכתב קובץ ההגדרה `.claude/agents/chen.md` עם YAML frontmatter (`name: chen`, `tools: WebSearch, WebFetch, Read, Write, Edit, Glob, Grep` — בלי Bash) ו-system prompt מלא בעברית. נוצרו `chen/.gitkeep` ו-`chen/Memory/searches.md` עם header התחלתי + תבנית פורמט. CLAUDE.md עודכן: חן מסומנת "פעילה" עם trigger keywords, נוסף סעיף "Pipeline: יצירת תוכן חדש מאפס" שמתאר את ה-flow המלא חן→יעל→יובל→ראובן. יעל עודכנה להתעלם מ-frontmatter של חן בקלט.
- **Decisions:**
  - **כלים:** WebSearch + WebFetch מ-Claude Code (לא Perplexity/Tavily — הם זמינים native). ה-placeholders ב-`.env.example` נשארים בהערה.
  - **זיכרון:** `chen/Memory/searches.md` עם פורמט קבוע, append-only, עם תג `[DYNAMIC]` לנושאים שדורשים cache invalidation מהיר. חן `Grep`-ים אותו לפני כל חיפוש.
  - **Content frontmatter:** קובצי המאמרים של חן מכילים `source_url`, `quality`, `dynamic` ועוד. יעל מתעלמת מה-frontmatter בעת השכתוב (תוקן ב-system prompt שלה).
  - **חן לא מנתבת:** אכיפה ברורה. ראובן הוא היחיד שמחליט על המשך ה-pipeline.
- **Notes / Caveats:** חן לא מכוונת לקרוא PDF מקומיים — רק URLs. WebFetch על paywalled sources יחזיר שגיאה — חן מטפלת בזה (חיפוש אלטרנטיבי, לא המצאה).
- **Related:** [[reuven]], [[yael]], [[project-infrastructure]]
