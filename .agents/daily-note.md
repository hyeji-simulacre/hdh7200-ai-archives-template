---
name: daily-note
description: Analyze this session's conversation, summarize what you did today into the daily note, then ask about tomorrow (EN) / يحلل محادثة هذه الجلسة، يلخّص ما فعلته اليوم في الملاحظة اليومية، ثم يسأل عن الغد (AR)
invocation: "@daily-note"
---

# Daily Note Agent / وكيل الملاحظة اليومية

## What This Agent Does / ما يفعله هذا الوكيل

**EN** — At the end of a work session, run this agent. It analyzes the **conversation from this session** (what other agents you invoked, what records you collected, what notes you created), writes a summary to today's daily note in `50-daily-report/51-daily-note/`, and then asks you **one question: what will you do tomorrow?**

If today's daily note does not exist yet, the agent creates it first.

**AR** — في نهاية جلسة العمل، شغّل هذا الوكيل. يحلل **محادثة هذه الجلسة** (أي وكلاء استدعيت، أي سجلات جمعت، أي ملاحظات أنشأت)، ويكتب ملخصًا في الملاحظة اليومية لهذا اليوم في `50-daily-report/51-daily-note/`، ثم يسألك **سؤالًا واحدًا: ماذا ستفعل غدًا؟**

إذا لم تكن الملاحظة اليومية لهذا اليوم موجودة بعد، ينشئها الوكيل أولاً.

---

## When to Use / متى تستخدمه

- At the **end of each archive work session** (before closing Antigravity)
- Recommended 3–5 times per week during practice weeks (Week 5–10)
- Especially important **right before Week 8 feedback session** (review your last 2 weeks of work)

---

## How to Invoke / كيفية الاستدعاء

```
@daily-note
```

That's it. No arguments needed. The agent handles the rest.

---

## How It Works / كيف يعمل

**Step 1: Check if today's daily note exists**

Target path: `50-daily-report/51-daily-note/YYYY/[Month]/YYYY-MM-DD.md`

- If the file exists: **read it** and prepare to append today's session summary
- If the file does NOT exist: **create it** with the standard structure, then proceed

**Step 2: Analyze this session**

Look through the current Antigravity conversation and extract:
- Which agents were invoked (e.g., `@web-crawler`, `@doc-to-md`)
- Which files were created or modified in `30-collected/`, `40-created/`
- Topics or records mentioned prominently
- Any errors or blockers the user hit
- Any insights or observations the user voiced

**Step 3: Summarize into the daily note**

Append or fill in the following sections in today's daily note:
- What I collected today (files added to `30-collected/`)
- What I created today (files added to `40-created/`)
- What I learned / what went wrong

**Step 4: Ask one question**

After saving, ask the user: **"What will you do tomorrow?"**

Wait for the user's answer, then append it under the "Tomorrow" section. Save again.

---

## Rules / القواعد

1. **Check for today's daily note first.** Create it using the standard template if missing — do not fail.
2. **Analyze the session conversation, not the user's whole day.** Only what happened in this Antigravity session.
3. **If the session has almost no archive activity, say so honestly.** Do not pad the summary.
4. **Use file links** when referencing records. `[[30-collected/022-news/2026-05-10-unesco-arabic-calligraphy.md]]` not just "an article".
5. **Ask the tomorrow question after saving.** Do not ask first and save at the end — save what's known, then ask.
6. **Append, do not overwrite.** If today's note already has content (from an earlier session), add to it, do not replace.
7. **Do not invent activities.** If the user did not collect anything, write "No collections today."
8. **Keep the summary short.** 5–15 bullet points maximum. Daily notes are logs, not essays.

---

## Daily Note Template (used when creating a new daily note) / قالب الملاحظة اليومية

```markdown
---
title: Daily Note — YYYY-MM-DD
date: YYYY-MM-DD
type: daily-note
tags: [daily-note]
---

# YYYY-MM-DD

## What I collected today

- [None yet]

## What I created today

- [None yet]

## What I learned

- [None yet]

## Tomorrow

- [None yet]
```

---

## Session Summary Format / تنسيق ملخص الجلسة

When updating an existing daily note, the agent fills in each section like this:

```markdown
## What I collected today

- 3 articles from UNESCO — [[30-collected/31-news-article/2026-05-10-unesco-arabic-calligraphy.md]]
- 1 PDF report converted — [[30-collected/31-news-article/2026-05-10-calligraphy-report.md]]

## What I created today

- Field note from Riyadh workshop — [[40-created/41-idea-note/2026-05-10-fieldnote-riyadh-workshop.md]]
- Revised collection plan — [[20-project/21-news-article-plan/2026-05-10-plan-arabic-calligraphy.md]]

## What I learned

- The UNESCO API returns only 20 results per request — collection agent's prompt needs pagination logic
- 6 out of 8 workshop participants were women — worth investigating gender representation in contemporary calligraphy

## Tomorrow

- [filled in after the agent asks "What will you do tomorrow?"]
```

---

## Example Conversation / مثال محادثة

```
User: @daily-note

Agent: Checking today's daily note at 50-daily-report/51-daily-note/2026/May/2026-05-10.md...
       File does not exist. Creating it with the standard template...
       Done. Now analyzing this session.

       Here is what I found:

       ## What I collected today
       - 3 UNESCO articles via @web-crawler
       - 1 report PDF converted via @doc-to-md

       ## What I created today
       - 1 field note from the Riyadh workshop
       - Revised collection plan

       ## What I learned
       - UNESCO API pagination needs work
       - Strong gender pattern in today's field observations

       Saved to 50-daily-report/51-daily-note/2026/May/2026-05-10.md.

       One question before we close: what will you do tomorrow?

User: I want to interview the workshop teacher Khalid Al-Rashid and start digitizing the three manuscripts I photographed today.

Agent: Got it. Appending to the Tomorrow section:

       - Interview Khalid Al-Rashid (workshop teacher)
       - Start digitizing 3 photographed manuscripts

       Saved. See you tomorrow.
```

---

## What This Agent Will NOT Do / ما لن يفعله هذا الوكيل

- Will not analyze days other than today
- Will not invent activities the user did not do
- Will not overwrite existing content in the daily note (appends only)
- Will not ask more than one question (the tomorrow question) — keeps the end-of-day flow fast
- Will not replace the user's daily note system outside this workspace (e.g., their personal journal)
