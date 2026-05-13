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

### 2026-05-13 — Yael handles Chen's frontmatter [shipped]
- **What was done:** נוספה הערה ב-system prompt של יעל (בתוך שלב "קריאת המאמר" ב-Flow העבודה) שמורה לה להתעלם מ-YAML frontmatter בקבצים שמקורם מ-[[chen]]. ה-rewrite מתחיל מתחת ל-frontmatter, מהכותרת `#` הראשונה. הפלט שלה לא כולל את ה-frontmatter — רק את התוכן ה-rewritten.
- **Decisions:** Frontmatter מצד חן הוא internal metadata (URL, איכות, תאריך). אין סיבה להחזיר אותו בפלט הסופי של יעל — הוא יישאר בקובץ ה-Content/ המקורי לתיעוד. אם המשתמש ירצה attribution בתוצר הסופי, ראובן יוסיף אותו בשלב ה-merge.
- **Notes / Caveats:** התוספת קצרה ולא משפיעה על Flow קיים — רק מנחה איך לטפל בסוג קלט חדש שמגיע מחן. יעל ממשיכה לעבוד גם על קבצים בלי frontmatter בדיוק כמו קודם.
- **Related:** [[chen]], [[reuven]]

### 2026-05-13 — Image placeholder protocol added [shipped]
- **What was done:** נוסף סעיף "## איתור מקומות לתמונה" ל-system prompt של יעל. יעל מתבקשת לזהות מקומות טבעיים לתמונה במאמר ולהשאיר `{{IMAGE_NEEDED: "<תיאור עם סגנון>"}}` ב-MD וב-HTML. בדיווח הסופי לראובן — רשימת ה-placeholders ממוספרת.
- **Decisions:** תחביר ה-placeholder אחיד ב-MD וב-HTML (טקסט גלוי, לא comment) — מקל על debug ועל פעולת ה-merge של ראובן. יעל לא מייצרת תמונות בעצמה — היא רק מציינת איפה צריך.
- **Notes / Caveats:** ב-HTML, ה-placeholder יוצג כטקסט גלוי לפני ההחלפה (לא ideal לתצוגה ביניים, אבל זה תוצר עבודה — הסופי יחליף את שני הצדדים). הסעיף החדש לפני "כללי שכתוב" ואחרי "Flow העבודה".
- **Related:** [[yuval]], [[reuven]], [[project-infrastructure]], [[skill-gpt-image-gen]]

### 2026-05-13 — First article rewrite: "מאמר CRM.txt" [shipped]
- **What was done:** שכתוב של מאמר CRM (15.6KB) מ-`Content/מאמר CRM.txt` לשני תוצרים ב-`Output/`: `Output/מאמר CRM.md` ו-`Output/מאמר CRM.html`. ההמרה ל-HTML בוצעה ידנית עם תבנית ה-RTL הקלאסית מתוך ה-system prompt של יעל (פונט סריפי-עברי, רוחב 720px, line-height 1.75, blockquote עם border-right, responsive). הקובץ נצפה ב-Launch preview panel של VS Code.
- **Decisions:**
  - **הוסר:** CTA אחרון של המחבר ("תכתבו לי כמה המאמר הזה עזר לכם"), הזכרת "תלמידים שלי" (קידום פלטפורמת הדרכה), name-drop "איתי זרם" בדוגמה (הוחלף ב"לקוח ספציפי"), אימוג'ים (😅, 🙂), כותרת כפולה אקראית ("מה זה מערכת CRM") שהופיעה באמצע הטקסט המקורי.
  - **נשמר:** סיפור הפיצה בשוהם (חלק מהסיפור), מותגים בתוך הסיפור (Make, WhatsApp, Excel, PowerPoint, Google Drive, GDPR), הכל ה-FAQ, הטון הכללי (B2B שיחתי-עברי).
  - **שינויים בעריכה:** הידוק חזרות, ניקוי מילים בלתי-נחוצות ("אשכרה היה מבאס" → "היה מבאס"), המרת WhatsApp/וואטסאפ לכתיב אחיד (WhatsApp באנגלית), שיפור היררכיית כותרות.
- **Notes / Caveats:**
  - **style-guide ו-reference היו ריקים** — כתבתי לפי שיקול דעת סביר (טון B2B שיחתי, פחות אימוג'ים, יותר הידוק). כשהמשתמש יכתוב את style-guide.md ההפעלה הבאה תוכל לסטות בכיוון אחר.
  - לא הופעל דרך Agent tool — `subagent_type=yael` לא חשוף ב-SDK הנוכחי. ראובן ביצע את הפרוטוקול ידנית עבור יעל.
- **Related:** [[reuven]], [[project-infrastructure]]
