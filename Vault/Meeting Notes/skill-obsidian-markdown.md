# Skill: obsidian-markdown

## Overview
סקיל מקומי תחת `.claude/skills/obsidian-markdown/SKILL.md` שמגדיר איך לכתוב Obsidian-flavored Markdown תקין: wikilinks (`[[Note]]`), embeds (`![[Note]]`), callouts (`> [!type]`), frontmatter עם properties, block IDs (`^block-id`), קישורי כותרות (`[[Note#Heading]]`), ועוד. תומך בעבודה השוטפת על ה-[[skill-obsidian-vault-workflow|vault]] — כל קובץ topic מנצל את התחביר הזה.

## Open Questions
- האם נצטרך גם callouts ייעודיים (`[!warning]`, `[!info]`) ב-topic files, או שמספיק טקסט רץ?
- אילו properties כדאי להוסיף לכל קובץ topic (tags, status, owner)?

## Session Log

### 2026-05-13 — Skill placed by user [shipped]
- **What was done:** ה-SKILL.md הוצב ע"י המשתמש ב-`.claude/skills/obsidian-markdown/`. לא בוצע שום שינוי בקובץ — רק תיעוד.
- **Decisions:** מוסכם שתחביר wikilinks (`[[]]`) יהיה הדרך היחידה לקישורים פנימיים ב-vault. קישורי Markdown סטנדרטיים (`[text](url)`) רק לקישורים חיצוניים.
- **Notes / Caveats:** הסקיל מפנה ל-references פנימיים (PROPERTIES.md, EMBEDS.md, CALLOUTS.md) שגם כן הותקנו עם המאגר.
- **Related:** [[skill-obsidian-vault-workflow]], [[skill-obsidian-bases]], [[project-infrastructure]]
