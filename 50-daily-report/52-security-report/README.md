# 52-security-report — Security Reports / تقارير الأمان

**EN** — Security-related logs: access log (who accessed restricted records), backup status, incident notes, fixity check results. One report per check cycle (weekly recommended).

**AR** — سجلات متعلقة بالأمان: سجل الوصول، حالة النسخ الاحتياطي، ملاحظات الحوادث، نتائج فحوصات السلامة.

---

## Template / القالب

```markdown
# Security Report — YYYY-MM-DD

## Backup Status
- Last backup: [date]
- Medium: [external HDD / cloud / etc.]
- Result: [OK / FAILED — reason]

## Fixity Check
- Records checked: [number]
- Mismatches: [number] — [details if any]

## Access Log
- Restricted records accessed: [list or "none"]

## Incidents
- [any security incidents or concerns]
```
