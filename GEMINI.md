# GEMINI.md — Master Configuration

> Antigravity reads this file first. It tells every agent about the workspace structure, shared rules, and the student's project context.

---

## Workspace Identity

- **Course**: Digital Archiving Systems — HDH 7200
- **Program**: Masters in Digital Heritage (MDH)
- **Institution**: Royal Institute of Traditional Arts × Korea National University of Cultural Heritage
- **Semester**: Year 1, Semester 2 (2026)
- **AI Platform**: Antigravity (Gemini)

---

## Folder Map

```
AI-Archives-Workspace-HDH7200/
├── .agents/                     # agent prompts
├── 00-system/                   # system operation
│   ├── 01-scripts/              # automation scripts
│   ├── 02-templates/            # template collection
│   └── 03-security/             # security (.env, tokens — gitignored)
├── 10-standards/                # standards & rules you adopt
│   ├── 11-metadata-standards/   # metadata standards (Dublin Core · RiC etc.)
│   └── 12-preservation-rules/   # preservation rules (format policy, backup)
├── 20-project/                  # your archiving plan
├── 30-collected/                # collection results (by record_type)
├── 40-created/                  # knowledge you produce
├── 50-daily-report/             # daily activity log
│   ├── 51-daily-note/           # daily notes
│   └── 52-security-report/      # security reports
└── 60-dev-project/              # development experiment (optional)
```

---

## Shared Rules for All Agents

1. **Language**: Write all outputs in **English**. If the student writes in Arabic, respond in Arabic, but default to English.
2. **File format**: All text records are **Markdown (.md)** with **YAML frontmatter**.
3. **Metadata standard**: Follow `10-standards/11-metadata-standards/ric-metadata.md` (RiC-CM) for every record.
4. **Preservation policy**: Follow `10-standards/12-preservation-rules/preservation.md` for format decisions.
5. **Access policy**: Follow `10-standards/12-preservation-rules/access-policy.md` for access level assignments.
6. **Source attribution**: Every collected record must include `source_url`, `access_date`, and `license`.
7. **No hallucinated metadata**: If you do not know a date, name, or URL, write `unknown` — never invent.
8. **No file deletion**: Never delete files. If a record needs replacing, create a new version and keep the old one.
9. **Record IDs**: Use the format `RIC-YYYY-NNNN` (zero-padded to 4 digits). Never reuse an ID.
10. **Save locations**:
    - External records → `30-collected/3X-[record_type]/`
    - Student-produced notes → `40-created/4X-[note_type]/`
    - Daily summaries → `50-daily-report/51-daily-note/YYYY-MM-DD.md`

---

## Student Project Context

> ⚠️ **Students: fill this section in Week 6 ("Feeding Standards").**

- **Heritage subject**: _[your cultural heritage topic]_
- **Type**: _☐ Tangible · ☐ Intangible · ☐ Mixed_
- **Region**: _[geographic focus]_
- **Time period**: _[time scope]_
- **Why this subject**: _[2–3 sentences]_

---

## Agent Inventory

| Agent | File | Role |
|---|---|---|
| Web Crawler | `.agents/web-crawler.md` | Collect web pages with source metadata |
| YouTube Transcript | `.agents/youtube-transcript.md` | Extract video transcripts |
| Doc-to-MD | `.agents/doc-to-md.md` | Convert PDF/DOCX to Markdown |
| Collection Plan | `.agents/collection-plan.md` | Draft a collection plan interactively |
| Field Note | `.agents/field-note.md` | Capture fieldwork observations |
| Insight Memo | `.agents/insight-memo.md` | Turn observations into analytical claims |
| Note Linker | `.agents/note-linker.md` | Suggest related notes |
| Daily Note | `.agents/daily-note.md` | Summarize today's session |
