---
title: Access & Rights Policy
type: policy
applies_to: all records
last_modified: 2026-04-26
status: active
related:
  - "[[../11-metadata-standards/ric-metadata.md]]"
  - "[[preservation.md]]"
---

# Access & Rights Policy / سياسة الوصول والحقوق

**EN** — Who can see what, under what conditions, and how do we prove it. This is the operating manual for Block 2 (Security) of Week 4, written as rules agents can apply.

**AR** — من يستطيع رؤية ماذا، تحت أي شروط، وكيف نثبت ذلك.

---

## 1. Three Access Levels / ثلاثة مستويات للوصول

Every record must have one of these three values in its `access_level` field:

| Level | Meaning | Examples |
|---|---|---|
| `public` | anyone can view, share, reuse within the license | published news articles, public exhibitions, government records released for public access |
| `restricted` | view only by approved researchers; request log required | records identifying minors, oral histories with named living individuals, donor-restricted collections |
| `confidential` | not viewable; metadata only; review by holder before any access | medical records, ongoing legal cases, records embargoed by donor |

**Default**: if you do not know, mark `restricted` and ask. Never default to `public`.

---

## 2. The Four Ethical Questions / الأسئلة الأخلاقية الأربعة

Before publishing any record as `public`, the collector must answer all four (Week 3 Slide F):

1. **Consent** — did the people in this record agree to this use? If they cannot be asked (deceased, anonymous), is there a clear public interest?
2. **Sensitivity** — does this record reveal information that could harm someone if seen out of context? (location of a private home, identity of a minor, religious or political affiliation)
3. **Ownership** — who owns the rights? Have we documented permission from them?
4. **Continuity** — will the rights situation still be acceptable 50 years from now? (e.g., a child in a 2026 photo will be an adult in 2050)

If any answer is "no" or "unclear," the access level is at most `restricted`.

---

## 3. Authentication, Authorization, Audit / المصادقة، التفويض، التدقيق

Three layers, three different questions:

| Layer | Question | Implementation in this workspace |
|---|---|---|
| **Authentication** (who are you?) | identity | the workspace lives on your machine; access is by OS user account |
| **Authorization** (what can you do?) | role | three roles: `viewer` (read-only), `editor` (read + write to `40-created/`), `admin` (full access incl. `01-standards/`) |
| **Audit** (what did you do?) | log | every access to a `restricted` or `confidential` record is logged in `../../00-system/03-security/access-log.md` |

In a personal student workspace you are usually all three roles. In a real institution, they are different people.

---

## 4. License Field — Allowed Values / قيم الترخيص المسموحة

| Value | Use when |
|---|---|
| `Public domain` | original is out of copyright (typically 70+ years after creator's death, varies by country) |
| `CC BY 4.0` | attribution required |
| `CC BY-NC 4.0` | attribution + non-commercial |
| `CC BY-NC-ND 4.0` | attribution + non-commercial + no derivatives |
| `CC0 1.0` | dedicated to public domain by holder |
| `All rights reserved` | default for copyrighted works without explicit license — collected for study, not redistribution |
| `Institutional license — see source` | when the holding institution has its own terms (cite `source_url`) |

**Rule**: if a record's `license` is `All rights reserved`, its `access_level` cannot be `public`. The two fields must be consistent.

---

## 5. Sensitive Content Categories / فئات المحتوى الحساس

Records that automatically receive `restricted` or `confidential` until reviewed:

- Records identifying **minors** (under 18) by name or face
- **Personally identifiable information** (national IDs, addresses, phone numbers, email)
- **Medical records** of identifiable individuals
- **Oral histories** where the speaker did not give explicit publication consent
- Records flagged by the holding institution as sensitive

The student is responsible for additional context-specific layers (religious, tribal, linguistic) that the policy cannot enumerate from outside.

---

## 6. PREMIS Events for Access / أحداث PREMIS الخاصة بالوصول

Every access to a `restricted` or `confidential` record generates a PREMIS event:

```yaml
event:
  eventType: "access"
  eventDateTime: "2026-04-26T14:32:00+03:00"
  eventOutcome: "granted | denied"
  linkingAgent: "user@institution"
  linkingObject: "RIC-2026-0007"
  reason: "research request — short description"
```

Stored in `../../00-system/03-security/access-log.md` (append-only).

---

## 7. What Agents Do With This File / ما يفعله الوكلاء بهذا الملف

- **`@web-crawler`** must read §4 before assigning a license; default to `All rights reserved` if not stated
- **`@doc-to-md`** must check §5 for sensitive content patterns and flag for review
- **All collection agents** must set `access_level` based on §1 and §2; never default to `public`

---

## Reference

- Society of American Archivists. *Code of Ethics*, 2020 revision.
- ICA. *Universal Declaration on Archives*.
- PREMIS Editorial Committee. *PREMIS Data Dictionary for Preservation Metadata*, v3.0.
