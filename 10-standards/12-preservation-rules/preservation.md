---
title: Preservation Policy for HDH 7200 Workspace
type: policy
applies_to: all records
last_modified: 2026-04-26
status: active
related:
  - "[[../11-metadata-standards/ric-metadata.md]]"
  - "[[access-policy.md]]"
  - "../00-system/backup-log.md"
---

# Preservation Policy / سياسة الحفظ

**EN** — This policy decides *what format we keep things in*, *how long*, and *what we do when a format ages*. It is the operating manual for Block 1 of Week 4 (Storage · Format Migration · Emulation), translated into rules your agents can follow.

**AR** — تحدد هذه السياسة *التنسيق الذي نحفظ به الأشياء*، *لمدة كم*، *وماذا نفعل عندما يتقادم التنسيق*.

---

## 1. Format Priorities / أولويات التنسيقات

For every record, keep a **master copy** in an open archival format and an **access copy** in a widely-used format.

| Record type | Master format (preserve forever) | Access format (share, view) |
|---|---|---|
| Text | Markdown (UTF-8), PDF/A | PDF |
| Image | TIFF (uncompressed) | JPG (quality ≥ 85) or PNG |
| Audio | WAV (PCM, 48kHz, 24-bit) or FLAC | MP3 (≥ 192 kbps) |
| Video | FFV1 in MKV (Matroska) | MP4 (H.264) |
| Structured data | JSON or XML (UTF-8) | CSV |
| Web page | WARC (Web ARChive) + Markdown extract | HTML |

**Never delete the master to save space.** Storage is cheaper than re-collecting.

---

## 2. Migration Schedule / جدول الترحيل

Migration happens for two reasons:

| Trigger | Action | Timeline |
|---|---|---|
| **Scheduled (calendar)** | Review every record's format | every 5 years |
| **Event-driven** | Vendor announces end-of-life, standard is deprecated, hardware no longer supports format | within 6 months of announcement |

Every migration must produce a **migration log entry** with:
- original format, original checksum (sha256)
- new format, new checksum (sha256)
- date, tool used, operator
- visual or aural verification result (the access copy still shows / sounds correct)

The log is a record itself. It lives in `../../00-system/migration-log.md`.

---

## 3. Emulation Decision Tree / شجرة قرار المحاكاة

When migration is **not** an option (interactive media, software-bound art, legacy OS records), use emulation:

```
Is the record interactive (game, CD-ROM, software-based art)?
  ├── Yes → emulate (do not migrate)
  └── No  → can the format be migrated to an open format without loss?
            ├── Yes → migrate (Section 2)
            └── No  → emulate, document the runtime
```

For emulation, document in the record's frontmatter:
- `emulator: "DOSBox 0.74-3" | "JSMESS" | "Internet Archive Emularity"`
- `runtime_environment: "MS-DOS 6.22, 640K RAM"`

---

## 4. Storage Tiers / مستويات التخزين

| Tier | Medium | What goes there | Access speed |
|---|---|---|---|
| Hot | local SSD inside `30-collected/` and `40-created/` | active working records | instant |
| Warm | external HDD or institutional cloud | full archive snapshot | minutes |
| Cold | LTO tape OR M-DISC OR cloud archive (Glacier-class) | locked masters, untouched for decades | hours to days |

Every record must reach the **warm** tier within 7 days of being collected.
Every record must reach the **cold** tier within 90 days.

---

## 5. Fixity Checks / فحوصات السلامة

A `sha256` checksum is computed when the record enters the archive (`checksum_sha256` field in RiC frontmatter).

| Tier | Fixity check frequency |
|---|---|
| Hot | quarterly |
| Warm | annually |
| Cold | every 5 years (or when retrieved) |

A failed fixity check means **silent corruption**. The record is restored from a backup copy and the failed copy is quarantined (moved to `../../00-system/03-security/quarantine/`), not deleted.

Each fixity check produces a PREMIS event entry (`fixityCheck` event type).

---

## 6. What Agents Do With This File / ما يفعله الوكلاء بهذا الملف

- **`@web-crawler`** reads §1 to choose the format to save in, §3 if the page is interactive
- **`@doc-to-md`** reads §1 to choose the master format, then converts to Markdown for working copy
- **`@field-note`** writes Markdown only (already master format)
- **All collection agents** must populate `file_format`, `preservation_format`, and `checksum_sha256` in the RiC frontmatter (see `../11-metadata-standards/ric-metadata.md`)

---

## Reference / المراجع

- Library of Congress. *Recommended Formats Statement*. 2024 edition.
- Digital Preservation Coalition. *Digital Preservation Handbook*, 2nd ed.
- ISO 14721 (OAIS Reference Model)
