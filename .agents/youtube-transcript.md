---
name: youtube-transcript
description: Extract transcripts from YouTube videos and save as Markdown records (EN) / يستخرج النصوص من فيديوهات يوتيوب ويحفظها كسجلات Markdown (AR)
invocation: "@youtube-transcript [YouTube URL]"
---

# YouTube Transcript Agent / وكيل نصوص يوتيوب

## What This Agent Does / ما يفعله هذا الوكيل

**EN** — Extracts the transcript (subtitles) of a YouTube video and saves it to your archive as a Markdown record. Preserves video metadata (title, channel, upload date, duration). Essential for archiving oral history, lectures, interviews, and cultural performances available on YouTube.

**AR** — يستخرج النص (الترجمة) لفيديو يوتيوب ويحفظه في أرشيفك كسجل Markdown. يحفظ البيانات الوصفية للفيديو (العنوان، القناة، تاريخ الرفع، المدة). ضروري لأرشفة التاريخ الشفهي والمحاضرات والمقابلات والعروض الثقافية المتاحة على يوتيوب.

---

## When to Use / متى تستخدمه

- Archiving interviews with cultural practitioners
- Collecting recorded lectures or documentaries
- Capturing performances of intangible heritage (songs, dances, crafts)
- Referencing video sources in your Papers

---

## How to Invoke / كيفية الاستدعاء

Single video:
```
@youtube-transcript https://www.youtube.com/watch?v=XXXXXXXXXXX
```

With language preference:
```
@youtube-transcript https://www.youtube.com/watch?v=XXXXXXXXXXX language=ar
```

---

## Rules / القواعد

1. **Only process videos with publicly available transcripts.** If no transcript exists (no auto-captions, no manual subtitles), stop and inform the user.
2. **Prefer manual/official transcripts over auto-generated.** Note the type in frontmatter.
3. **Preserve timestamps** for videos longer than 5 minutes. Short videos can be saved as running text.
4. **Record language(s)** accurately. A video may have Arabic audio + English auto-caption — flag this.
5. **Always record**: video URL, title, channel name, upload date, duration, transcript language, transcript type (manual / auto).
6. **Do not translate.** If the transcript is Arabic, keep it Arabic. Translation is a separate task.
7. **Respect copyright.** Note in frontmatter: "YouTube videos retain creator copyright. Use for research only, do not redistribute."
8. **Save to `30-collected/32-interview-video/`** by default. If the video is not an interview but a documentary, lecture, or performance, ask the user whether to save to `32-interview-video/` anyway or create a new sub-folder (e.g., `35-video-lecture/`, `36-performance/`).

---

## Output Format / تنسيق المخرجات

Save to: `30-collected/32-interview-video/YYYY-MM-DD-channel-short-title.md` (or another `30-collected/3X-*/` sub-folder if the video is not an interview)

```markdown
---
title: [video title]
source_url: [YouTube URL]
channel: [channel name]
upload_date: [YYYY-MM-DD]
duration: [HH:MM:SS]
language: [ar / en / other]
transcript_type: [manual / auto-generated]
access_date: [YYYY-MM-DD]
license: youtube-standard (creator copyright)
collection_method: youtube-transcript
type: video-transcript
tags: [tag1, tag2]
---

# [Video Title]

**Channel**: [name]
**Duration**: [HH:MM:SS]
**Language**: [language]

---

## Transcript

[00:00] First line of transcript...
[00:15] Second line...
...

---

## Source Note

- Retrieved from [URL] on [access_date]
- Transcript type: [manual / auto-generated]
- Copyright belongs to the video creator. Use for research only.
```

---

## Example / مثال

Invocation:
```
@youtube-transcript https://www.youtube.com/watch?v=exampleID
```

Output file: `30-collected/32-interview-video/2026-05-12-unesco-arabic-calligraphy-documentary.md`

---

## What This Agent Will NOT Do / ما لن يفعله هذا الوكيل

- Will not download the video itself (only the transcript text)
- Will not translate between languages
- Will not process private or unlisted videos without transcript access
- Will not bypass YouTube's rate limits
