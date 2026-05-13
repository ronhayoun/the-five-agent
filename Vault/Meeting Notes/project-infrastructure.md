# Project Infrastructure

## Overview
המבנה הבסיסי של הפרויקט: `CLAUDE.md` בשורש (ייצוג של [[reuven]]), תיקיית `.claude/` עם תתי-תיקיות (`agents/`, `skills/`, `commands/`), קבצי תשתית ([[env-files]], [[gitignore]]), תיקיית `Vault/` (התיעוד הזה), ותיקיית `.obsidian/` (הגדרות אפליקציית Obsidian).

`.claude/agents/` מכיל כעת **שלושה סוכנים פעילים**: [[yael]], [[yuval]], ו-[[chen]] — צוות שלם. `.claude/commands/` עדיין ריקה. `.claude/skills/` מכיל ארבעה סקילים פרויקטיאליים ([[skill-obsidian-vault-workflow]], [[skill-obsidian-markdown]], [[skill-obsidian-bases]], [[skill-gpt-image-gen]]) + 14 סקילים מ-superpowers (ראו [[superpowers-installation]]).

בשורש הפרויקט תיקיות עבודה לכל הסוכנים: `yael/` (סגנון + reference), `yuval/` (reference + outputs), `chen/` (Memory/searches.md לוג חיפושים פרסיסטנטי), `Content/` (קלט ליעל — חן שומה לכאן את ה-extracts שלה), `Output/` (תוצרים סופיים — MD + HTML + `images/<slug>/`).

ה-pipeline המלא של הצוות (כפי שמוגדר ב-CLAUDE.md): **חן** מוצאת מקור → **יעל** משכתבת + מסמנת `{{IMAGE_NEEDED}}` → **יובל** מייצר תמונות → **ראובן** מדביק הכל ל-`Output/` self-contained.

## Open Questions
- האם נשמור את ה-`.gitkeep` ב-`commands/` או נסיר אותו כשנמלא אותה?
- האם `commands/` יקבל פקודות slash מותאמות בהמשך (למשל `/research`, `/write`, `/illustrate`)?
- האם להוסיף סקיל ייעודי ל-pipeline orchestration (`run-content-pipeline`)?

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

### 2026-05-13 — Chen + full content pipeline activated [shipped]
- **What was done:** נכתב הסוכן השלישי [[chen]] (`.claude/agents/chen.md`) עם `WebSearch`/`WebFetch` + זיכרון פרסיסטנטי ב-`chen/Memory/searches.md`. נוצרה תיקיית `chen/` עם header של searches.md ותבנית פורמט. CLAUDE.md הורחב עם סעיף "Pipeline: יצירת תוכן חדש מאפס (חן → יעל → יובל)" שמתאר 3 ה-pipelines האפשריים (חן בלבד, חן→יעל, חן→יעל→יובל) + טבלת דוגמאות לפענוח בקשות. [[yael]] עודכנה להתעלם מ-frontmatter של חן בקלט.
- **Decisions:**
  - **3 סוכנים פעילים** — צוות שלם. אין יותר placeholders ב-`.claude/agents/`.
  - **WebSearch/WebFetch native** — לא Perplexity/Tavily. הפלייסהולדרים ב-`.env.example` נשארים בהערה.
  - **Cache strategy:** חן בודקת `chen/Memory/searches.md` לפני כל חיפוש; 30 ימים לנושאים יציבים, אפס cache לנושאים דינמיים ([DYNAMIC] tag).
  - **Frontmatter במצב כלאיים** — חן כותבת YAML frontmatter ב-Content/<slug>.md, יעל מתעלמת ממנו בשכתוב. שני הסוכנים יודעים את הקונבנציה.
  - **חן לא מנתבת** — היא רק מכינה קרקע (extract → `Content/`) ומדווחת. ראובן בלבד מחליט על המשך ה-pipeline.
- **Notes / Caveats:** Pipeline orchestration על ראובן: לכל סוכן Agent tool call נפרד. חן יכולה לעצור באמצע (cache hit) ולחזור לראובן עם שאלה — צריך לתמוך בהמשך אינטראקטיבי. לא נבדק E2E עדיין.
- **Related:** [[reuven]], [[chen]], [[yael]], [[yuval]], [[skill-gpt-image-gen]]
