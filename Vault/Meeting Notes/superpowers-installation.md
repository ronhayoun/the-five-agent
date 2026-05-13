# Superpowers Installation

## Overview
התקנה ידנית של ה-plugin [obra/superpowers](https://github.com/obra/superpowers) v5.1.0 (Jesse Vincent) לפרויקט. ההתקנה נעשתה ע"י clone ל-temp והעתקת `skills/` בלבד אל `.claude/skills/` (במאגר אין `commands/` או `agents/`). 14 סקילים נכנסו לפרויקט וזמינים לכל הצוות: [[reuven]], [[yael]], [[yuval]], [[chen]].

הסקילים: brainstorming, dispatching-parallel-agents, executing-plans, finishing-a-development-branch, receiving-code-review, requesting-code-review, subagent-driven-development, systematic-debugging, test-driven-development, using-git-worktrees, using-superpowers, verification-before-completion, writing-plans, writing-skills.

## Open Questions
- האם נצטרך לעדכן כשתצא גרסה חדשה של superpowers (5.2+)? אם כן — באיזה אופן (rebase, fresh-clone, sync script)?
- האם להפוך חלק מהסקילים ל-default invoke ב-CLAUDE.md (למשל `using-superpowers` בתחילת כל סשן)?

## Session Log

### 2026-05-13 — Manual install of 14 skills [shipped]
- **What was done:** Clone של `obra/superpowers` ל-temp, `cp -rn` של `skills/` אל `.claude/skills/`. ה-`.gitkeep` הקיים נשמר (no-clobber). Commit ו-push ל-`origin/main`.
- **Decisions:** התקנה ידנית בלבד — לא דרך `/plugin` (לא זמין במערכת המקומית). שימוש ב-`cp -n` כדי לא לדרוס קבצים קיימים.
- **Notes / Caveats:** Commit hash: `8cb3b12`. אזהרות LF/CRLF התקבלו (התנהגות רגילה ב-Windows). תיקיית temp נמחקה.
- **Related:** [[project-infrastructure]], [[reuven]]
