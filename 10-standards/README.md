# 10-standards — Standards & Rules You Adopt / المعايير والقواعد التي تتبناها

**EN** — The **reference knowledge** your agents use to make decisions: metadata standards, preservation rules, access policies, and ethical principles. "Feeding standards to agents" (Week 6) means pointing them to this folder.

**AR** — **المعرفة المرجعية** التي يستخدمها الوكلاء لاتخاذ القرارات: معايير الوصف، قواعد الحفظ، سياسات الوصول، والمبادئ الأخلاقية.

---

## Sub-folders / المجلدات الفرعية

| Folder | Purpose (EN) | الغرض (AR) | Assignment Step |
|---|---|---|---|
| `11-metadata-standards/` | Metadata standards (Dublin Core · RiC · PREMIS etc.) | معايير الوصف | Step 5, 6 |
| `12-preservation-rules/` | Preservation rules (format policy, backup policy, access policy) | قواعد الحفظ | Step 3, 5 |

---

## How Agents Use This Folder / كيف يستخدم الوكلاء هذا المجلد

When you "feed standards" to an agent in Week 6, you write a prompt that says: *"Before you act, read the relevant files in `10-standards/` and follow them."*

- The **collection agent** reads your chosen metadata standard before writing records.
- The **daily-note agent** follows the template format.
- All agents check the access policy before assigning `access_level`.

**Without standards, agents guess. With standards, they follow your rules consistently.**
