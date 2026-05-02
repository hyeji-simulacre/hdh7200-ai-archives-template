---
title: RiC-CM Metadata Profile for HDH 7200
type: standard
standard: Records in Contexts — Conceptual Model (RiC-CM v1.0.2, ICA EGAD)
applies_to:
  - 30-collected/
  - 40-created/
last_modified: 2026-04-26
status: active
---

# RiC Metadata Profile / ملف بيانات RiC الوصفية

**EN** — Every record in `30-collected/` and `40-created/` follows the **Records in Contexts** (RiC) model published by the International Council on Archives. RiC describes records, the agents who create them, the activities they document, and the relations between them. Use the YAML frontmatter below as a sidecar for every record.

**AR** — كل سجل في `30-collected/` و `40-created/` يتبع نموذج **السجلات في سياقاتها** (RiC) الصادر عن المجلس الدولي للأرشيف. يصف RiC السجلات والعملاء الذين ينشئونها والأنشطة التي توثقها والعلاقات بينها.

---

## Why RiC, not Dublin Core / لماذا RiC وليس Dublin Core

| Concern | Dublin Core (15 fields) | RiC-CM |
|---|---|---|
| Captures **context** (provenance, custody) | weak | strong |
| Captures **relations** between records | none | first-class |
| Captures **activities and agents** separately | no | yes |
| Designed for archives | no (general) | yes |

**EN** — Dublin Core is fine for a single object in a library. An archive needs to keep the *web* of context around a record: who created it, in what activity, under whose custody, related to which other record. RiC was built for that.

**AR** — Dublin Core يكفي لوصف عنصر واحد في مكتبة. الأرشيف يحتاج إلى الحفاظ على *شبكة* السياق حول السجل.

---

## Core Entities Used in This Workspace

We use **5 of the 7** RiC entities in this course. The other two (`Mandate`, `Rule`) are advanced.

| Entity | Plain meaning | Where it shows up |
|---|---|---|
| **Record** | the thing itself (image, document, audio) | the file in `30-collected/` |
| **Record Set** | a group of related records | a subfolder like `021-artifact/` |
| **Agent** | a person, organization, or software that created or held the record | `creator:` field, `custodian:` field |
| **Activity** | what was being done when the record was created | `activity:` field (e.g., "field visit", "exhibition") |
| **Place** | where the record was created or where the activity happened | `place:` field |

---

## Required Frontmatter / البيانات الإلزامية

Every record file (or its sidecar `.md`) must include this YAML block at the top:

```yaml
---
# RiC Record
record_id: RIC-2026-NNNN              # internal stable ID
record_type: artifact | news | photograph | oral-history | document
title: "Human-readable title"
title_ar: "العنوان بالعربية"             # optional but recommended
language: ar | en | mixed
date_created: YYYY-MM-DD               # when the original was created
date_collected: YYYY-MM-DD             # when YOU collected it into this archive

# RiC Agents
creator:                               # who made the original record
  - name: "Creator name"
    type: person | organization
custodian:                             # who currently holds it (where you got it)
  - name: "Holding institution"
    type: organization
collected_by: "Your name"              # the student / archivist

# RiC Activity
activity: "field visit | web collection | digitization | interview"

# RiC Place
place:
  name: "Riyadh, King Abdulaziz Public Library"
  country: "Saudi Arabia"

# Source & Rights
source_url: "https://..."              # if collected from the web
source_citation: "Full citation"
license: "CC BY 4.0 | CC BY-NC | All rights reserved | Public domain"
rights_holder: "Name of rights holder"
access_level: public | restricted | confidential

# Preservation
file_format: jpg | tiff | pdf | mp3 | wav | mp4
file_size_mb: 0.0
checksum_sha256: "abc123..."
preservation_format: "TIFF (master) + JPG (access)"

# Relations (RiC's strength)
related_records:                       # other RIC IDs this connects to
  - id: RIC-2026-0002
    relation: "is-part-of"             # is-part-of | derived-from | created-during | references | succeeds
  - id: RIC-2026-0007
    relation: "references"

# Subjects & Description
subjects:
  - "Arabic calligraphy"
  - "Thuluth script"
description: |
  One paragraph. What is this record? Why did you collect it?

# Workflow
status: draft | reviewed | published
tags:
  - calligraphy
  - heritage
---
```

---

## Field-by-Field Notes / ملاحظات حقل بحقل

- **record_id** — Use `RIC-YYYY-NNNN`. Pad to 4 digits. Never reuse an ID.
- **creator vs custodian** — *Creator* made the record (e.g., a 14th-century calligrapher). *Custodian* is who holds it now (e.g., the King Abdulaziz Public Library). They are usually different.
- **activity** — Pick the activity *that produced this record into your archive*. For a web crawl, that is "web collection." For a museum visit, it is "field visit."
- **related_records** — This is what makes RiC powerful. List every record this one connects to, with the **relation type**. Five common relations:
  - `is-part-of` — this record belongs to a larger record set
  - `derived-from` — this record was created from another (e.g., a translation, a digitization)
  - `created-during` — this record was created during the same activity as another
  - `references` — this record cites or refers to another
  - `succeeds` — this record replaces a previous version
- **access_level** — Default to `public`. Mark `restricted` if it shows minors, identifies private individuals, or if the holding institution restricts use. See `access-policy.md`.

---

## Minimum Required Fields / الحد الأدنى المطلوب

If you cannot fill everything, fill at least these eight:

1. `record_id`
2. `record_type`
3. `title`
4. `date_created` (or `date_collected` if creation date unknown)
5. `creator` OR `custodian` (one of the two)
6. `source_url` OR `source_citation`
7. `license`
8. `description`

A record without these eight cannot be promoted from `draft` to `reviewed`.

---

## Reference / المراجع

- ICA EGAD. *Records in Contexts — A Conceptual Model for Archival Description* (RiC-CM v1.0.2). 2023.
- ICA EGAD. *Records in Contexts — Ontology* (RiC-O v1.0). 2023.
