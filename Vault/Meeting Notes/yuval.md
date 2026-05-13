# יובל — מעצב התמונות

## Overview
יובל הוא sub-agent **פעיל** של מעצב התמונות. קובץ ההגדרה ב-`.claude/agents/yuval.md`. תפקידו: לקבל בקשת תמונה מראובן, לקרוא reference מ-`yuval/reference/` (לחילוץ סגנון/פלטה/אווירה), לנסח prompt באנגלית שמשלב בין הבקשה לסגנון, לקרוא ל-API של OpenAI דרך הסקיל [[skill-gpt-image-gen]], ולשמור PNG + sidecar `.txt` ב-`yuval/outputs/<YYYY-MM-DD>-<slug>.png`. הכלים שלו: `Read, Write, Bash, Glob` (Bash דרוש ל-curl). דורש `OPENAI_API_KEY` ב-[[env-files|.env]]. שותפים: [[yael]] ב-pipeline משולב של מאמרים עם תמונות (יעל משאירה `{{IMAGE_NEEDED}}`, יובל ממלא, ראובן מדביק); [[chen]] בעתיד תספק רפרנסים. **המודל הוא `gpt-image-2` — אסור לשנות.**

## Open Questions
- האם להוסיף תמיכה במספר תמונות ב-API call יחיד (לחיסכון בקריאות), או להשאיר 1:1 כדי לפשט?
- האם להוסיף Gemini כ-fallback אם OpenAI לא זמין? (כרגע לא — `# GEMINI_API_KEY` נשאר בהערה ב-`.env.example`)
- האם הסגנון הראשוני יוגדר ע"י המשתמש (placement ב-`yuval/reference/`), או שיובל יתחיל מסגנון default?

## Session Log

### 2026-05-13 — Role placeholder created [planned]
- **What was done:** יובל מופיע ברשימת הצוות ב-CLAUDE.md ובאינדקס ה-vault. ב-`.env.example` שמורים placeholders ל-`OPENAI_API_KEY` ו-`GEMINI_API_KEY` כצפי לשימוש שלו.
- **Decisions:** טרם הוחלט על ספק תמונות, פרומפט מערכת, או רשימת כלים.
- **Notes / Caveats:** הסוכן ייכתב בהמשך הסדנה.
- **Related:** [[reuven]], [[yael]], [[chen]], [[env-files]]

### 2026-05-13 — Yuval agent activated [shipped]
- **What was done:** נכתב קובץ ההגדרה `.claude/agents/yuval.md` עם YAML frontmatter (`name: yuval`, `tools: Read, Write, Bash, Glob`, description עם trigger keywords) ו-system prompt מלא בעברית. נוצרו תיקיות עבודה: `yuval/`, `yuval/reference/`, `yuval/outputs/` (כולן עם `.gitkeep`). הוסר ה-comment מ-`OPENAI_API_KEY` ב-`.env` וב-`.env.example`. נכתב הסקיל [[skill-gpt-image-gen]] עם curl template + Python fallback ל-decode. CLAUDE.md עודכן: יובל מסומן "פעיל" עם trigger keywords, נוסף סעיף "Pipeline: מאמר עם תמונות" שמתאר את ה-flow ביבול ↔ יובל ↔ ראובן.
- **Decisions:**
  - **מודל:** `gpt-image-2` — קבוע. אסור לשנות. הערה בולטת גם ב-SKILL.md וגם ב-yuval.md למניעת drift.
  - **Tools:** Read/Write/Bash/Glob. Bash חובה ל-curl. Glob ל-scan של reference.
  - **Outputs naming:** `<YYYY-MM-DD>-<slug>.png` עם sidecar `.txt` שמכיל את הפרומפט המלא + רשימת references. חיוני לאיטרציה.
  - **Pipeline merge:** ראובן מעתיק PNG מ-`yuval/outputs/` ל-`Output/images/<article-slug>/` (לפי החלטת המשתמש) — Output/ נשמר self-contained.
- **Notes / Caveats:** הסקיל כולל source ל-`.env` אוטומטי אם `$OPENAI_API_KEY` לא מוגדר ב-shell. Python fallback לעקוף את חסר jq ב-Git Bash. בדיקת end-to-end דורשת OPENAI_API_KEY אמיתי — המשתמש יבדוק.
- **Related:** [[reuven]], [[yael]], [[skill-gpt-image-gen]], [[env-files]], [[project-infrastructure]]
