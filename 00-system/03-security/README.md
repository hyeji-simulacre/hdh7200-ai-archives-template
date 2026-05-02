# 03-security — Security / الأمان

**EN** — Security-sensitive files: `.env` files, API tokens, credentials. **This folder is gitignored** — nothing here is pushed to GitHub. If you need to share tokens with a teammate, use a secure channel, never GitHub.

**AR** — الملفات الحساسة أمنيًا: ملفات `.env`، رموز API، بيانات الاعتماد. **هذا المجلد مستبعد من Git** — لا يُرفع شيء منه إلى GitHub.

---

## What Goes Here

- `.env` — environment variables (API keys, model preferences)
- `*.token` — authentication tokens
- `*.key` — encryption keys

> ⚠️ **Never commit these files to GitHub.** The `.gitignore` at the root already excludes them.
