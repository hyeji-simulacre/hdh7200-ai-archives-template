---
name: BEST_PRACTICES
description: Guidelines for writing and using AI agents in this workspace
---

# Agent Best Practices / أفضل الممارسات للوكلاء

**EN** — This document defines how agents in this workspace are written, invoked, and maintained. Read this before editing any agent file.

**AR** — تحدد هذه الوثيقة كيفية كتابة الوكلاء في مساحة العمل هذه واستدعائهم وصيانتهم. اقرأ هذا قبل تعديل أي ملف وكيل.

---

## Common Template / القالب المشترك

Every agent file in this folder follows this structure:

كل ملف وكيل في هذا المجلد يتبع هذه البنية:

```markdown
---
name: agent-name
description: One-line description (EN / AR)
invocation: "@agent-name" or specific trigger phrases
---

# Agent Name / اسم الوكيل

## What This Agent Does / ما يفعله هذا الوكيل
One paragraph in EN + one paragraph in AR.

## When to Use / متى تستخدمه
Bullet list of situations.

## How to Invoke / كيفية الاستدعاء
Exact phrase the user types, or `@agent-name` in Antigravity chat.

## Rules / القواعد
Numbered rules the agent must follow.

## Output Format / تنسيق المخرجات
Template or schema the agent produces.

## Example / مثال
One worked example.
```

---

## Naming Convention / قواعد التسمية

- Agent file name: `kebab-case.md` (e.g., `web-crawler.md`, not `WebCrawler.md` or `web_crawler.md`)
- `name:` field in frontmatter matches the file name without `.md`
- Invocation phrase uses the same name: `@note-linker`, `@web-crawler`

---

## Writing Rules / قواعد الكتابة

**EN**

1. **Keep agents focused on one job.** An agent that does too many things becomes unreliable.
2. **Write rules in imperative form.** "Always include the source URL" not "sources should be included."
3. **Specify the output format exactly.** If you want YAML frontmatter + markdown body, say so and show an example.
4. **Tell the agent what NOT to do.** Negative rules prevent surprises.
5. **Use EN/AR for user-facing strings, EN only for internal rules.** Internal rules need only one language for consistency.
6. **Reference `10-standards/` for policies, not inline.** Agents should read standards at runtime, not have them baked in.

**AR**

1. **اجعل الوكلاء مركّزين على مهمة واحدة.** الوكيل الذي يقوم بأشياء كثيرة يصبح غير موثوق.
2. **اكتب القواعد بصيغة الأمر.** "ضمّن رابط المصدر دائمًا" وليس "يجب تضمين المصادر".
3. **حدد تنسيق المخرجات بدقة.** إذا كنت تريد YAML + markdown، قل ذلك واعرض مثالاً.
4. **أخبر الوكيل بما يجب ألا يفعله.** القواعد السلبية تمنع المفاجآت.
5. **استخدم الإنجليزية والعربية للنصوص الموجهة للمستخدم، والإنجليزية فقط للقواعد الداخلية.**
6. **أشر إلى `10-standards/` للسياسات، لا تضمّنها داخل الوكيل.**

---

## Running an Agent in Antigravity / تشغيل وكيل في Antigravity

**EN**

1. Open Antigravity and open this workspace folder
2. In chat, type `@agent-name` followed by your request
   - Example: `@web-crawler please collect articles about Arabic calligraphy from UNESCO`
3. The agent reads its own `.md` file and follows the rules inside
4. Review the output. The agent may write files to `30-collected/`, `40-created/`, or `50-daily-report/51-daily-note/`
5. If the output is wrong, refine your request or edit the agent's rules

**AR**

1. افتح Antigravity وافتح مجلد مساحة العمل هذه
2. في المحادثة، اكتب `@اسم-الوكيل` متبوعًا بطلبك
3. يقرأ الوكيل ملف `.md` الخاص به ويتبع القواعد بداخله
4. راجع المخرجات. قد يكتب الوكيل ملفات إلى `30-collected/` أو `40-created/` أو `50-daily-report/51-daily-note/`
5. إذا كانت المخرجات خاطئة، حسّن طلبك أو عدّل قواعد الوكيل

---

## Safety Rules / قواعد السلامة

**EN**

- **Never let an agent delete files** unless you explicitly tell it to, and confirm the path
- **Never overwrite originals.** If an agent converts a file, keep the original
- **Always review agent output before citing it in your Papers**
- **AI agents can hallucinate metadata.** Check dates, names, and URLs manually

**AR**

- **لا تدع الوكيل يحذف الملفات أبدًا** إلا إذا أخبرته بذلك صراحةً، وأكد المسار
- **لا تستبدل الأصول أبدًا.** إذا حوّل الوكيل ملفًا، احتفظ بالأصل
- **راجع دائمًا مخرجات الوكيل قبل الاستشهاد بها في أوراقك**
- **يمكن لوكلاء الذكاء الاصطناعي اختلاق البيانات الوصفية.** تحقق من التواريخ والأسماء والروابط يدويًا

---

## Editing an Agent / تعديل وكيل

**EN** — You may edit agent files starting from Week 6 ("Feeding Standards"). Back up the original file before editing. If your edit breaks the agent, restore from the GitHub template repo.

**AR** — يمكنك تعديل ملفات الوكلاء بدءًا من الأسبوع 6 ("تغذية المعايير"). احتفظ بنسخة احتياطية قبل التعديل. إذا كسر تعديلك الوكيل، استعِد من مستودع GitHub النموذجي.
