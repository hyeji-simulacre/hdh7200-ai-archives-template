---
name: doc-to-md
description: Convert PDF and other document formats to Markdown records (EN) / يحوّل PDF وتنسيقات المستندات الأخرى إلى سجلات Markdown (AR)
invocation: "@doc-to-md [file path]"
---

# Document to Markdown Agent / وكيل تحويل المستندات إلى Markdown

## What This Agent Does / ما يفعله هذا الوكيل

**EN** — Converts PDF, DOCX, and other document files into Markdown records in your archive. Extracts text, preserves structure (headings, lists, tables), and attempts OCR if the PDF is image-based. Saves the converted file to `30-collected/` with full source metadata.

**AR** — يحوّل ملفات PDF و DOCX وتنسيقات المستندات الأخرى إلى سجلات Markdown في أرشيفك. يستخرج النص، يحافظ على البنية (العناوين، القوائم، الجداول)، ويحاول التعرف الضوئي على الحروف (OCR) إذا كان PDF قائمًا على الصور. يحفظ الملف المحوّل في `30-collected/` مع البيانات الوصفية الكاملة للمصدر.

---

## Supported Formats / التنسيقات المدعومة

| Input format | Conversion method | Notes |
|---|---|---|
| PDF (text-based) | Direct text extraction | Fastest, highest fidelity |
| PDF (image-based) | OCR | May have errors, especially for Arabic — verify |
| DOCX, DOC | Document parser | Tables and images preserved |
| PPTX | Slide extraction | Each slide as a section |
| XLSX | Table extraction | Each sheet as a Markdown table |
| RTF, ODT | Standard parsers | |

> **Note / ملاحظة**: For Korean HWP/HWPX files, this agent does not support them. Those require a specialized Korean document converter.

---

## When to Use / متى تستخدمه

- Digitizing scanned documents from physical archives
- Converting institutional PDF reports into searchable archive records
- Extracting tables from PDF research papers
- Converting Word documents shared by interview subjects

---

## How to Invoke / كيفية الاستدعاء

Single file:
```
@doc-to-md please convert /path/to/report.pdf
```

With OCR for scanned PDF:
```
@doc-to-md /path/to/scan.pdf ocr=true language=ar
```

Batch:
```
@doc-to-md convert all PDFs in /path/to/folder/
```

---

## Rules / القواعد

1. **Keep the original file.** Never delete or modify the source document.
2. **Save conversion to `30-collected/`.** Use an appropriate subfolder (`024-documents/` if none exists).
3. **Always record**: original filename, file format, file size, conversion date, conversion method (direct / OCR), OCR confidence (if applicable), language.
4. **For OCR output, flag low-confidence sections.** Mark unclear passages with `[unclear]` so the user knows to verify.
5. **Preserve page numbers** in the output for PDFs. Format: `--- Page N ---`.
6. **Extract tables as Markdown tables**, not as images or raw text.
7. **For Arabic documents**: use right-to-left-aware OCR and preserve Arabic characters exactly. Do not transliterate.
8. **Do not auto-translate.** Convert is a format change, not a language change.

---

## Output Format / تنسيق المخرجات

Save to: `30-collected/024-documents/YYYY-MM-DD-original-filename.md`

```markdown
---
title: [document title or original filename]
source_file: [original filename]
source_format: [pdf / docx / pptx / xlsx]
source_size: [bytes]
pages: [number of pages, if applicable]
author: [if known]
document_date: [YYYY-MM-DD, if known]
conversion_date: [YYYY-MM-DD]
conversion_method: [direct / ocr]
ocr_language: [ar / en / mixed, if OCR used]
ocr_confidence: [high / medium / low, if OCR used]
language: [ar / en / other]
license: [if known, else "unknown"]
collection_method: doc-to-md
type: document
tags: [tag1, tag2]
---

# [Document Title]

--- Page 1 ---

[Content of page 1...]

--- Page 2 ---

[Content of page 2...]

---

## Source Note

- Original file: [filename]
- Conversion method: [direct / ocr]
- [If OCR]: Some passages marked [unclear] — verify against original
```

---

## Example / مثال

Invocation:
```
@doc-to-md /Users/student/Desktop/calligraphy-report-2024.pdf
```

Output file: `30-collected/024-documents/2026-05-08-calligraphy-report-2024.md`

---

## What This Agent Will NOT Do / ما لن يفعله هذا الوكيل

- Will not delete or modify source files
- Will not translate content
- Will not process encrypted or password-protected files
- Will not convert HWP/HWPX (Korean documents) — use a specialized tool
- Will not guarantee OCR accuracy for handwritten or damaged documents
