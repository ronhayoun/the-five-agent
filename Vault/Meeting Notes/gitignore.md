# `.gitignore`

## Overview
קובץ ה-`.gitignore` בשורש הפרויקט מגדיר מה לא נכנס ל-Git. תפקידו העיקרי כאן: להגן על `.env` (ראו [[env-files]]) מפני דחיפה בטעות ל-GitHub. בנוסף הוא מוסתיר קבצי OS (`.DS_Store`, `Thumbs.db`), הגדרות IDE (`.vscode/`, `.idea/`), ו-`*.log`.

## Open Questions
- כשנוסיף תיקיית `output/` או `temp/` לתוצרים של הסוכנים (תמונות שיובל יוצר, דוחות של חן) — האם להחביא אותן מ-Git או לדחוף את ההיסטוריה?
- האם כדאי להוסיף `node_modules/` בהמשך אם נכניס Node?

## Session Log

### 2026-05-13 — Initial gitignore created [shipped]
- **What was done:** נוצר `.gitignore` עם 5 קבוצות: env files, OS files, IDE configs, logs.
- **Decisions:** הוספת דפוס `.env.*.local` כדי לתמוך בעתיד גם בקבצי env לפי סביבה.
- **Notes / Caveats:** אומת שאחרי `git status` הקובץ `.env` לא מופיע ברשימת untracked.
- **Related:** [[env-files]], [[project-infrastructure]]
